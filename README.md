# Conduit - AI Augmented Feature Development

In this assessment, you will work on a realistic task that closely resembles issues you may face on the job. Your challenge in this assignment is to guide GPT to extend an existing project with a new feature. This repository contains the project to be extended, which is a full-stack TypeScript application consisting of a NestJS backend and an Angular frontend.

Your submission should not reflect the capabilities of the AI but should showcase your skills in guiding and leveraging it to fulfill the given requirements. Make sure to provide instructions and context to the AI based on your knowledge, ensuring that the output is technically sound and adheres to typical engineering standards and practices. Ultimately, the solution generated must be something you are comfortable attaching your name to and should represent a joint effort between your expertise and the AI's capabilities. This assessment uses a stack similar to our projects and we welcome you to leverage AI to fill any knowledge gaps. 

If you believe success hinges primarily on familiarity with specific technologies, this role may not align with your approach.

## Assessment Steps

1. [Start the code in Gitpod](#running-in-gitpod), and take a look at [the feature requirements](#feature-the-conduit-roster) and [the grading criteria](#evaluation-criteria) described below. 
1. Use the GPT interface linked on the Crossover assessment to perform most of the research, design, write new code, etc. 
   - Imagine that GPT is a "junior" with little context about the project, but good general technical knowledge. 
   - We have included built-in prompts with general information about the project in the chat interface. Feel free to leverage these prompts.
1. Perform the necessary code adjustments to fulfill the requirements of the feature.
1. [Submit your work](#submitting-your-work) by following the instructions below.

*Note: The project doesn't include tests, and you're not required to write any.*

## Running in Gitpod

You can sign up for a free Gitpod account here: https://www.gitpod.io/ using your GitHub account. After you sign up, open the following link to launch your environment: https://www.gitpod.io/#https://github.com/trilogy-group/ws-eng-conduit-ai-assessment/tree/rwa/feature-development-v3

Gitpod offers a browser-based VSCode interface with pre-configured terminal tasks to seed the database and start the application. Here, "localhost" refers to the remote machine. All "localhost" ports are exposed to a Workspace-specific URL, which is automatically opened if you press any localhost link from the Gitpod terminal, output pane, editor, etc. To open the UI, you can press the `http://localhost:4200/` link in the App terminal (printed once the Angular app spins up) or, alternatively, you can type `gp url 4200` in a new terminal to find the URL manually.

If you are inactive for a while, your Workspace will be "paused". All file changes that you have made to the repository will be saved. You can resume it by refreshing the link or by going here: https://gitpod.io/workspaces. Lastly, if you need to upload a file from your local machine, simply drag and drop the file or right click on the folder --> Upload.

Some Firefox users face a "Security Error" when opening Gitpod; see [this issue for details and workarounds](https://github.com/gitpod-io/gitpod/issues/9386).

This project can also be [run locally](./LOCAL.md); this will require up to 60 minutes of set-up time.

**Hints**:
- You can access the UI at http://localhost:4200 and log in with `jcosten0@purevolume.com` / `password`.
- You can also find the backend API spec at http://localhost:3000/docs.
- You can run nx commands (e.g., for generating components) by running `npm run nx -- <command here>`, e.g., `npm run nx -- g @nx/angular:library something`.

## Feature: The Conduit Roster 
**Summary**: As a reader, I want to view a rank-ordered list of authors, such that I can find and follow the most popular authors on the site.

**Requirements**:
 - [Already Done] Create a new Roster page and link it in the top navigation after the "Home" page link. 
 - On this page, include the following:
 - A "Conduit Roster" header,
 - A table containing the stats for each user as described below.
 - The stats would contain:
    - The user name & profile link,
    - The total number of articles authored (zero if none),
    - The total number of favorites received on their articles (zero if none),
    - The date of their first posted article (empty if no article was posted yet).
 - This table should be statically sorted based on the number of favorites received. 

**Acceptance Test**:
1. Given that you are logged in (any user),
1. When you open the "Roster" page,
1. Then you see all the Conduit users with correct stats sorted correctly,
1. When you create a new article,
1. And you open the "Roster" page,
1. **Screenshot**: Then you see your total number of articles incremented accordingly.

## Submitting your Work
1. Capture screenshots that show that the acceptance tests pass and place them directly in the `submission` folder in your repository.
1. Export the chat sessions used to build the feature and place them directly in the `submission` folder in your repository.
1. Do NOT create subfolders in the `submission` folder. Please all of your files directly in this folder.
1. Run `npm run submit` and follow the instructions.

## Evaluation Criteria
 - **Correctness & Completeness**: The final code should be functional, produce the desired output without significant errors, defects, or limitations, and address all the requirements, with minimal inconsistencies between requirement specifications and outputs (e.g., related to behavior, formatting, etc.).
 - **Code Quality**: The code to fix the issues should be clean, efficient, consistent with the provided code, respect the existing architecture and responsibility decomposition, and adhere to typical SOLID coding practices, REST API design principles, and relational database best practices.
 - **AI Usage**: The AI should be guided properly, by giving appropriate context, clear inputs, instructions, and feedback. 
