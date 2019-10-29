# Making modern resume

*How to make a modern responsive resume, edit with Jekyll and host it using GitHub pages for **free**.*

![responsive resume](https://github.com/mang0g0rilla/EgorZakharov.github.io/blob/master/readme_data/Front.JPG)

In this tutorial I will explain how to make your resume look modern and responsive on different screens using custom Jekyll theme. We will see how to edit the theme depending on our needs and add custom blocks. We will then publish the resume on GitHub pages for free.

# Audience

# Prerequisites

* Some experience with Markdown
* A GitHub account (which is free to make)
* A resume prepared in Word or similar software
* A little of patience and enthusiasm

# Installation
This installation tutorial is intended to Windows users. This process may be different for MacOS.
In our project we are going to use <mark>Ruby</mark>, <mark>Git</mark> and <mark>Jekyll</mark>. As a configuration management framework we are goint to use PowerShell from Microsoft which is basically a command line.

#### Step 1 - Download Ruby
* Download [Ruby](https://rubyinstaller.org/downloads/) and install it on your machine (if you have not done it previously)

#### Step 2 - Download Git
* Download [Git](https://git-scm.com/downloads) and install it on your machine (if you have not done it previously)

#### Step 3 - Download Jekyll
* Launch PowerShell by clickgin `Win+S` and typing `PowerShell`
* Run the following command: `gem install jekyll bundler`

## Run jekyll locally

#### Step 1 - Download the theme
* Download .zip containing the [theme](https://github.com/sproogen/modern-resume-theme/archive/gh-pages.zip)
* Extract to a new folder on your computer

#### Step 2 - Run the site locally
The following operations are to be done using PowerShell
* `cd [your_new_folder_with_Jekyll_theme`]
* `bundle install`
* `bundle exec jekyll serve`
* Open your browser to [http://localhost:4000](http://localhost:4000)

Now you will be able to see the preconstructed web page which should look as follows:

![Pre-build Resume](https://github.com/mang0g0rilla/EgorZakharov.github.io/blob/master/readme_data/pre-built.JPG)

# Usage

Now as you set up the environment and launch the site locally, you can edit, add new files to the project and see the changes immediatelly.

In this project you are going to edit data in .yml files which may seem unfamiliar. Feel free to use Markdown rools in these files.

#### _config.yml
This file contains the main configuration of the page. Feel free to replace all the personal information by your own.
* Use `Ctrl+/` to exclude the fields you don't need
* Change the avatar by placing your own picture into `images` folder and changing `about_profile_image: images/[your_avarat].jpg` field.
* Feel free to modify `more_content` section or delete it if not needed.

#### _layouts/default.html
This file contains the page layout. If you want to change the order of the sections or add a new one (later in this tutorial), you will have to modify the following code:

``` html
{%- include about.html -%}

{%- if site.data.education.size > 0 -%}
    {%- include education.html -%}
{%- endif -%}

{%- if site.data.projects.size > 0 -%}
    {%- include projects.html -%}
{%- endif -%}

{%- if site.data.experience.size > 0 -%}
    {%- include experience.html -%}
{%- endif -%}

{%- include more.html -%}
```

This modification brings the **education** section to the top of the page, right after the **about** section

#### _data folder
This folder contains **.yml** files of all the custom sections included in the resume.
* Open each file to replace any personal information by your own.
* Copy and paste the contents of a **section** as many times as you need if you had multiple job positions or university degrees.
* Leave a field blank if you don't need it (it will not appear in the document).
* Use options: `left`, `right`, `top`, `top-right` and `top-middle` in `-layout:` field to arrange the contents in the best way.

If you have multiple job titles at the same company, use the following fromat:

``` yml
- layout: left (options: left, right, top, top-right, top-middle)
  company: Company name
  link: Link to company (optional)
  jobs:
    - title: Job title 1
      dates: Date Range (eg. November 2016 - present)
    - title: Job title 2
      dates: Date Range (eg. January 2015 - November 2016)
  quote: >
   Short description of the company (optional)
  description: | # this will include new lines to allow paragraphs
    Description of role
```

# Custom sections
In case you may need a custom section which is not provided by default, or you want to modify the appearance of existing one, you have this functionality as well.

In this example you will see how to bring new section called **Skills**.

In order to create a new custom section **Skills** you need:
* Create a folder `_includes` at the root of the project
* Create `skills.html` inside `_includes` using the following format:

``` html
<div class="container container-skills">
    <h3>{{ site.skills_title | default: "Skills" }}</h3>
    {% for skill in site.data.skills %}
      {% include {{ skill.layout | default: 'left' | append: ".html" }} item=skill %}
    {% endfor %}
  </div>
```

* Create `skills.yml` in `_data` folder which should include the following fields:

``` yml
- layout: (left, right, top, top-right, top-middle)
  name: # What kind of skills is it?
  qualification: # your qualifivcation
  quote: # anything can go here
  description: # the descriptions of your skills
```

* Add a record about **Skills** section in `_layouts/default.html`

``` html
  {%- if site.data.skills.size > 0 -%}
    {%- include skills.html -%}
  {%- endif -%}
```

If you are familiar with <mark>SCSS</mark> or <mark>CSS</mark>, you can modify the `assets/main.scss` file to add new styles.

# Publishing resume

#### Step 1 - Create new repository
* Log in into GitHub or create a new account for **free**
* Create [new repository](https://github.com/new) and call it `[your_name].github.io`. **This is important since we are going to publish this repository**.

#### Step 2 - Upload project files
Using PowerShell:
* Stop the server by clicking `Ctrl+C`
* `git init`
* `git add .`
* `git commit -m "Initial commit"`
* `git remore add origin [your_repo_link]`
* `git push -u origin master`

#### Step 3 - publish
* Go to your repository on GitHub
* Click **Settings** on the toolbar
* Scroll until **GitHub Pages** section
* Choose **master branch** under the **Source**

Now you may visit your resume from any device using the link from above the **GitHub Pages** section.

# More resources
* Here is a [link](https://github.com/sproogen/modern-resume-theme) to the theme author's repository
* Here is a [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [Jekyll](https://jekyllrb.com/) web page
* Windows [PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/getting-started/getting-started-with-windows-powershell?view=powershell-6) docs

# Authors and Acknowledgements
* Thnaks to [James Grant](https://github.com/sproogen) for creating modern-resume-theme that we used in this project.

# FAQ's
#### Why does GitHub Pages gives me a 404 error?
Make sure your repository name ends with `.github.io`. It is required for your page to be published

#### How can I know which classes to select while applying custom SCSS styles?
Try using inspection tool in your browser to find elements you want to customize.

#### Why I dont see the changes after modifying the document?
You probably made a syntax error in the file you modified. Check **indentation** and the correctness of your code.

#### How can I know `my_repo_link` to upload project files?
Go to your repository. You will se a green button "Clone or Download" above the files. You will see the link once you click the button.