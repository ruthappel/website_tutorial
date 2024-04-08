# Creating your own website using GitHub Pages

Tutorial by Ruth Appel, December 1, 2023

- [**Background**](#background)

- [**Prerequisites**](#prerequisites)

- [**Create your website**](#create-your-website)

  - [Step 1: Copy the template](#step-1-copy-the-template)

  - [Step 2: Personalize your website](#step-2-personalize-your-website)

  - [Step 3: Set up the environment](#step-3-set-up-the-environment)

  - [Step 4: Deploy your website](#step-4-deploy-your-website)
    
  - [Step 5: Update your website](#step-5-update-your-website)

- [**Install additional dependencies**](#install-additional-dependencies)

- [**Further resources**](#uploading-files)

## Background

- This tutorial will walk you through how to use a website template and GitHub Pages to create your own website, and how to personalize it

- The main files you need to interact with are [Markdown](https://www.markdownguide.org/getting-started/) files. These are easier to read and edit than html code. The website template we will use uses Jekyll to transform markdown documents into html pages

- Once your website content is ready, you will commit it to a public GitHub repository and connect it to GitHub Pages, which will deploy your website

- You don't need any programming experience. Note that the more closely you follow the instructions, the less likely you are to run into errors

## Prerequisites

- You need a [GitHub](https://github.com/) account (basic version free; pro version free for students)

- You need to have other requirements installed (e.g., Ruby, Bundle, and Python), but you don't necessarily need to install them all separately, you can instead use [Docker](https://docs.docker.com/get-docker/), which will download everything you need. Instructions below will assume you use Docker. When you download Docker, you might have to create a free personal account for it to work

- Optional, but easier if you are not familiar with command lines: install [GitHub Desktop](https://desktop.github.com/) to sync content between GitHub and your local machine

- Optionally, if you don't yet have a convenient interface to show Markdown files, I recommend [Microsoft Visual Studio](https://visualstudio.microsoft.com/), which renders various code files nicely and makes editing them easier

## Create your website

### Step 1: Copy the template

- Navigate to [https://github.com/alshedivat/al-folio](https://github.com/alshedivat/al-folio)

- Click on **Use this template → Create a new repository**

![image1](https://github.com/ruthappel/website_tutorial/assets/40501125/7c25cfb6-0f0b-424e-8daf-447c1affbe68)

- Create a new public repository

    - If you want to host the site via GitHub Pages, your **repository name needs to be `[your-GitHub-username].github.io`**, e.g. if my GitHub username is ruthappel, the repo name needs to be ruthappel.github.io

- Clone the repository to your local computer (i.e., create a local copy in the directory where you want your website info to live). You can do this using the command line or by downloading GitHub Desktop and using the [GitHub Desktop user interface](https://docs.github.com/en/desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop)

    - ⚠️ You could also first create a new repository with your own name, and later copy the contents of the template over locally. However, if you do that, you need to be careful to copy over hidden files as well, without which website compilation will not work (you can show hidden files on Mac using `. + cmd + shift`)

    - ⚠️ You will be able to delete some template content that you don't need, but better don't delete any pages whose purpose you don't fully understand (e.g., be careful about deleting any page in the **`_layouts`** folder)

### Step 2: Personalize your website

- To see what you want to personalize, first check out what the website looks like when it's not personalized

    - Navigate to [https://alshedivat.github.io/al-folio/](https://alshedivat.github.io/al-folio/) to see what the template looks like as a website

    - Alternatively, go to the first steps in the deployment section below ([Step 4](#step-4-deploy-your-website)) and open a local copy of what your current website looks like

- The first file to edit is **_config.yml** in the main directory of the repository

    - Be sure to edit your name (`first_name`, `middle_name`, `last_name`) and `email`

    - Set `url` to your URL, e.g. `https://ruthappel.github.io`, and leave `baseurl` empty

    - If you want to edit the small icon displayed in the browser tab with your website name, edit the `icon` (you can enter e.g. an emoji or provide your own image in the `assets/img` folder)

    - In the `Social Integration` section, comment out or delete social media links you don't want to add, and add your usernames to the ones you do want to add

    - In the `Collections` section, comment out sections you might not want to use (e.g., if you don't add news or announcements, comment these out)

    - You can comment out the `Jekyll Archives` section if you don't plan on including a blog

    - In the `Jekyll Scholar` section

        - Update your name

        - Ensure that the name of the bibliography you'll upload matches the bibliography name in the template (i.e., `papers.bib`)

        - If you want your publications ordered in a specific way, you can specify this in the `group_by` field

        - More details and options for Jekyll scholar are [here](https://github.com/inukshuk/jekyll-scholar)

    - If you don't want to provide a resume in JSON format and e.g. just upload a PDF, comment out the `Get external JSON data` section

- Next, read through and customize the files in the **`_pages`** folder

    - You can delete pages you don't want, but likely you want to keep (and potentially edit) at least the following

        - **`about.md`** (e.g., add your profile text that will be displayed on the homepage here; add your profile picture by uploading a picture named `prof_pic.png` to the `assets/img` folder

        - **`cv.md`** (e.g., add name for the PDF CV you might want to upload to the `assets/pdf` folder)

        - **`Publications.md`** (you might not have to edit this)

- Publications

    - For your publications to show up, you need to edit the **`papers.bib`** in the `_bibliography` folder

    - Remove the default publications and add your own publications in BibTeX format. If you want a link to the paper to show up, add the URL to the custom `html` field

    - If you want to highlight a selected publication, you have to add the option `selected = {true}`

      ![image2](https://github.com/ruthappel/website_tutorial/assets/40501125/3e782e70-ac13-4337-8ab2-aa49a3073c71)

    - Easy ways to generate BibTeX citations

        - If you already use Zotero or Mendeley, you can export citations in BibTeX format using these citation managers

        - Otherwise, you can go to your publications online, most publishers allow you to copy citations in different formats

- If you want to change not the content, but the way it is displayed on your website, you need to edit the files in the **`_layouts`** or the **`_includes`** folder

    - E.g., if you want to not have your first name in your description on the home page bolded, you need to remove `<span class="font-weight-bold">` and `</span>` from the line `{% if site.title == "blank" -%}<span class="font-weight-bold">{{ site.first_name }}</span> {{ site.middle_name }} {{ site.last_name }}{%- else -%}{{ site.title }}{%- endif %}`

    - E.g., if you want to not have your first name in your page header bolded, you need change `<span class="font-weight-bold">{{- site.first_name -}}&nbsp;</span>` to `{{- site.first_name -}}&nbsp;`

- To change colors, you might have to change CSS files. The most relevant files are located in the **`_sass`** folder

    - E.g., if you want to change the color of most text on the website, you can edit the `global-theme-color` and `global-hover-color` fields in the `_themes.scss` file

- If you want to restrict how your website might be scraped, you have to edit the `robots.txt` file

- It can be tricky to figure out which file you need to edit to get a desired change. Here are some tips to find out what you need to edit

    - Google the theme and your question with the keyword "al folio" to see if someone else had the same question related to the template before

    - Open the template website (or your modified version if you modified it) in your browser. Right click on the element you want to change and click **Inspect** (for Chrome; might have a slightly different name in other browsers). This will open up the html code of the page, and you can look for hints where the thing you want to change is located. E.g., if you wanted to know where your profile picture was drawn from, if you inspect the picture, the html will highlight a section that shows that it's sourced from `assets/img`

     ![image3](https://github.com/ruthappel/website_tutorial/assets/40501125/6720431e-0ed1-49f2-83d3-27b9e0b61744)

   - Another option (also great for customization inspiration) is to compare what other people changed in their repositories for their desired result. You can look at other scholars' pages, e.g. (and I don't know them, just found them via Google) Kai Wu ([website](https://imkaywu.github.io/), [GitHub repo](https://github.com/imkaywu/imkaywu.github.io) for website) and Sebastian Koehler ([website](https://sebastiankoehler.eu/), [GitHub repo](https://github.com/sebkoehle/sebkoehle.github.io)). Note that the latter page is redirected from a personal domain to the GitHub pages site, the [template](https://github.com/alshedivat/al-folio/tree/master) website has instructions on how to set up your own domain when using a website template

### Step 3: Set up the environment

- Open the terminal 

- Navigate to the directory where your website repository lives. You can use the `cd` command to do that, e.g.

  `cd /Users/ruth/Documents/Website/ruthappel.github.io`

- Make sure that Docker is running (or that all other dependencies have been installed according to the [legacy setup option described in the template](https://github.com/alshedivat/al-folio/tree/master)). Run the following command to install all required dependencies

  `docker compose pull`
    
### Step 4: Deploy your website

- In the terminal, make sure you are in the repository for your website (see [Step 3](#step-3-setup-the-environment))

- Ensure Docker is running (or that all other dependencies have been installed)

- Run the following command to run your website

  `docker compose up`
    
    - ⚠️ Note that if you run into errors here, you need to fix them before deployment will work. Try to check the error messages in your terminal for hints what went wrong

- If you use Docker, you're now able to check a local version of your website before you push it to GitHub. Your console output should look something like the following, and you can just extract the server address and enter it in your web browser to see what your website would look like

  ![image4](https://github.com/ruthappel/website_tutorial/assets/40501125/bfee18b9-ae9d-47b5-b8eb-7cf23a730fb9)

- If you are happy with the website, you can now actually make it public. You can stop Docker from running by entering `ctrl + c`

- The template allows for automatic deployment that is triggered whenever you commit updates to your GitHub repository. You need to enable GitHub Actions in order to do that. To enable automatic deployment:

    - Go to your GitHub repository in a browser
    
    - Navigate to the Actions tab and enable GitHub Actions if they aren't enabled yet (you do not need to create any workflow)
    
    - Then go to the Settings tab and enable the following permissions  (Allow actions, give read and write permissions)

![image5](https://github.com/ruthappel/website_tutorial/assets/40501125/ec77b643-33c0-4806-b671-aeee026c7908)

- Now, commit your changes to your GitHub repository, e.g. via GitHub Desktop or the command line

    - This should automatically trigger website deployment, and you can monitor whether the deployment succeeds in the Actions tab of your repo
    
    - If your deployment fails, check the error messages in the Actions tab for hints what might have gone wrong

- When you see that the deployment succeeded and finished, your website should be online at **`[your-GitHub-username].github.io`**

- You should now also see a new branch in your repo called `gh-pages`. To finish setting up automate deployment for future commits, go to the Settings of your repo, choose the Pages section in the left hand menu, and set the branch for build and deployment to **`gh-pages`**

### Step 5: Update your website  

- If you want to update your website, you can follow the same instructions in [step 4](#step-4-deploy-your-website)

- Commit your updates to the `main` branch of your GitHub repository

- If you run into issues with your Gemfile, check whether the original `Gemfile.lock` is modified when you run Docker. If so, try committing only changes to other files, but not of the `Gemfile.lock` to GitHub and see if deployments works in that case

## Install additional dependencies

- In case you want to use additional functionalities that are not yet included, you might have to update the Gemfile

    - E.g., if you want to add functionality for additional PDF embedding, you could add the gem jekeyll-pdf-embed. To do so, you have to add the line

        `gem 'jekyll-pdf-embed'`
        
      in your Gemfile, and add the line
        
        `- jekyll-pdf-embed`
        
      to the Plugins subsection of the Jekyll settings section in **`_config.yml`**

- Make sure that your set up your environment after this again (run `docker compose pull` and `docker compose up` as before)

## Uploading files

- If you want to upload files and link to files on your own website, you can copy them into the assets directory and appropriate subdirectory

- Once you push your changes to GitHub, your new files will be uploaded as well

- They will be accessible via an URL corresponding to the directory where you uploaded them, only relative to your website, such as `https://ruthappel.github.io/assets/pdf/new_upload.pdf`

## Further resources

- The [template](https://github.com/alshedivat/al-folio/tree/master) website has great instructions
- [Jekyll scholar overview](https://github.com/inukshuk/jekyll-scholar)
- You can also check out this [video](https://www.youtube.com/watch?v=g6AJ9qPPoyc) (note that the video doesn't use Docker)
