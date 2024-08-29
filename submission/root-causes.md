# Root Causes

Please copy-paste the final answer that you obtained from the AI for each question. The chat interface has a copy button that you can use to copy each message in Markdown format. Please do NOT include images or screenshots.

## Problem 1

**Problem**: The tags are broken up into individual characters on the post view page.

**Question**: What is the underlying issue that causes this problem to occur and from which component (file) of this project does this issue originate?

**Answer**: * Article entity was not correctly handling an array of strings, split by commas and trimmed for whitespace
if (typeof dto.tagList === 'string' ) {
      article.tagList = dto.tagList.split(',').map(tag => tag.trim());
    } else if (Array.isArray(dto.tagList)) {
      article.tagList = dto.tagList.map(tag => tag.trim());
    }

    if (typeof articleData.tagList === 'string') {
      articleData.tagList = articleData.tagList.split(',').map((tag: string) => tag.trim());   
    } else if (Array.isArray(articleData.tagList)) {
      articleData.tagList = articleData.tagList.map((tag: string) => tag.trim());
    }

    readonly tagList: string[] | string;

*


## Problem 2

**Problem**: New tags  are not shown on the home page under "Popular Tags", even after a page refresh.

**Question**: What is the underlying issue that causes this problem to occur and from which component (file) of this project does this issue originate?

**Answer**: *In tag.service, there was no defined method for fetching the popular tags.
async findPopularTags(): Promise<ITagsRO> {
    const tags = await this.tagRepository.findAll({ orderBy: { popularity: 'desc' } });
    return { tags: tags.map(tag => tag.tag) };
  }
  
  @Get('popular')
  async findPopularTags(): Promise<ITagsRO> {
    const tags = await this.tagService.findPopularTags();
    return { tags };
  }

    @Get('popular')
  async findPopularTags(): Promise<ITagsRO> {
    return this.tagService.findPopularTags();
  }

  import { Injectable } from '@angular/core';
import { ComponentStore } from '@ngrx/component-store';
import { HttpClient } from '@angular/common/http';
import { tap } from 'rxjs/operators';

interface HomeState {
  tags: string[];
}

@Injectable()
export class HomeStoreService extends ComponentStore<HomeState> {
  readonly tags$ = this.select(state => state.tags);

  constructor(private readonly http: HttpClient) {
    super({ tags: [] });
  }

  readonly setTags = this.updater((state, tags: string[]) => ({
    ...state,
    tags,
  }));

  readonly fetchTags = this.effect<void>(trigger$ =>
    trigger$.pipe(
      tap(() => {
        this.http.get<{ tags: string[] }>('/api/tags/popular').subscribe(response => {
          this.setTags(response.tags);
        });
      })
    )
  );
}


import { Component, OnInit, ChangeDetectionStrategy } from '@angular/core';
import { UntilDestroy, untilDestroyed } from '@ngneat/until-destroy';
import {
  articleListInitialState,
  articleListQuery,
  articleListActions,
  ListType,
} from '@realworld/articles/data-access';
import { selectLoggedIn } from '@realworld/auth/data-access';
import { CommonModule } from '@angular/common';
import { TagsListComponent } from './tags-list/tags-list.component';
import { ArticleListComponent } from '@realworld/articles/feature-articles-list/src';
import { HomeStoreService } from './home.store';
import { provideComponentStore } from '@ngrx/component-store';
import { Store } from '@ngrx/store';

@UntilDestroy()
@Component({
  selector: 'cdt-home',
  standalone: true,
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css'],
  imports: [CommonModule, TagsListComponent, ArticleListComponent],
  providers: [provideComponentStore(HomeStoreService)],
  changeDetection: ChangeDetectionStrategy.OnPush,
})
export class HomeComponent implements OnInit {
  listConfig$ = this.store.select(articleListQuery.selectListConfig);
  tags$ = this.homeStore.tags$;
  isAuthenticated = false;

  constructor(private readonly store: Store, private readonly homeStore: HomeStoreService) {}

  ngOnInit() {
    this.store
      .select(selectLoggedIn)
      .pipe(untilDestroyed(this))
      .subscribe((isLoggedIn) => {
        this.isAuthenticated = isLoggedIn;
        this.getArticles();
      });

    // Fetch popular tags when the component initializes
    this.homeStore.fetchTags();
  }

  setListTo(type: ListType = 'ALL') {
    this.store.dispatch(articleListActions.setListConfig({ config: { ...articleListInitialState.listConfig, type } }));
  }

  getArticles() {
    if (this.isAuthenticated) {
      this.setListTo('FEED');
    } else {
      this.setListTo('ALL');
    }
  }

  setListTag(tag: string) {
    this.store.dispatch(
      articleListActions.setListConfig({
        config: {
          ...articleListInitialState.listConfig,
          filters: {
            ...articleListInitialState.listConfig.filters,
            tag,
          },
        },
      }),
    );
  }
}


import { Component, Input, ChangeDetectionStrategy } from '@angular/core';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'cdt-tags-list',
  standalone: true,
  template: `
    <div class="tag-list">
      <a *ngFor="let tag of tags" (click)="selectTag(tag)" class="tag-pill tag-default">
        {{ tag }}
      </a>
    </div>
  `,
  styleUrls: ['./tags-list.component.css'],
  imports: [CommonModule],
  changeDetection: ChangeDetectionStrategy.OnPush,
})
export class TagsListComponent {
  @Input() tags: string[] = [];

  selectTag(tag: string) {
    // Emit an event or call a method to filter articles by the selected tag
  }
}

<div class="home-page">
  <div class="tag-list">
    <cdt-tags-list [tags]="(tags$ | async) || []"></cdt-tags-list>
  </div>
  <div class="col-md-9">
    <cdt-article-list [config]="(listConfig$ | async)"></cdt-article-list>
  </div>
</div>

  *

