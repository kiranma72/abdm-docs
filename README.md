# ABDM Docs - README

This is the repository for the new ABDM sandbox documentation currently under development. 
You can preview the documentation produced by this repo at [https://kiranma72.github.io/abdm-docs](https://kiranma72.github.io/abdm-docs)

If you want to contribute to improving the documentation, write with your github id to kiranma@gmail.com and we will add you as a collabrator to this project 

## For contributors

- This documentation uses [Hugo](https://gohugo.io) to build the final documentation site. 
- We recommend [installing hugo](https://gohugo.io/installation/) on your local machine if you are making changes across multiple pages 
- You can clone this directory to your system using git clone --recursive https://github.com/kiranma72/abdm-docs/ 
- The folder structure is very important. All pages are under the directory "content". 
- Familiarize your self with how [Hugo organizes content](https://gohugo.io/getting-started/)
- Each folder under content represents a chapter
- The _index.md page contains the content for the chapter's starting page
- You can add as many pages to a chapter or create a new folder to create a sub-chapter
- The order of the pages are controlled by the "weight" parameter in the header of each page
- All pages are written using Markdown - Editor: [dillinger markdown editor](https://dillinger.io) and [Markdown Cheatsheet](https://www.markdownguide.org/cheat-sheet/)
- [Sublime Text Editor](https://www.sublimetext.com/) is recommended for use to edit Markdown content on your local system
- The content uses [Mermaid](https://mermaid.js.org/) for sequence diagrams. If you change the theme ensure it supports mermaid 
- Put images and other resources under the static folder. If you add to static folder reference your image using a path like /abdm-docs/img/<filename>
- Put images in the same content folder as the page your are editing. Reference the image using the path ../<filename> 
  
### How to make a contibution
We prefer that you make a Pull Request for your contribution. There are two ways to do that - 1) Using Github CLI 2) Using Github Website. For both the options, we prefer that you fork this repo, make changes onto your clone, and subsequently make a PR to this repo. Alternatively, if you have commit access to this repo, we would still prefer that you create a specific branch, make the changes and raising a PR. Directing committing to the main, should be your last option even if you have commit access. 

#### Using Github CLI
- If you prefer this, we assume that you are already familiar with github essentials. 
- Fork this repo, clone your newly created repo on local, make changes on master or a branch, commit and push to your repo
- Now raise a PR from your repo following [this process](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork)
  
#### Using Github Website
- login to Github
- Browse to this repository - https://github.com/kiranma72/abdm-docs
- Select and open the file you want to edit (e.g. README.md) 
- Edit (pencil icon) and make changes
- Once done, scroll down to the "Commit Changes" section. Specify a title and description (optional) and choose "Create a new branch for this commit and start a pull request" by selecting the "propose changes" option. 
  

## Documentation Output 
Every time you checkin / update a file on this project, an action is automatcially run (see the Github Actions tab). Hugo is used to build the final documentation set and this is pushed back into the repository under the **gh-pages** branch. 

To deploy the final site on your own domain you can fetch the **gh-pages** branch  
