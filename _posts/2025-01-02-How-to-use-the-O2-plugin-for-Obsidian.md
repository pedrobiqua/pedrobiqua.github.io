---
layout: post
category: Blog
title: "How to use the O2 plugin for Obsidian"
tags: [O2]
---

## What is this plugin for?

![image](/assets/img/2025-01-02-How-to-use-the-O2-plugin-for-Obsidian/Pasted-image-20250102180559.png)

This plugin converts Obsidian Markdown into a format compatible with platforms like Jekyll and Docusaurus. This is necessary because the formatting and usage of Markdown in these platforms are different.

## How to use it?

### 1. Installation

Using O2 is very simple. First, you need to install it. The plugin is available in the community plugins page, is free to use, and open-source. You can access the source code at [https://github.com/songkg7/o2](https://github.com/songkg7/o2). The plugin is maintained by Haril Song.

### 2. Activating the plugin

After downloading, simply activate the plugin. Check the image below to see how to do this.

![image](/assets/img/2025-01-02-How-to-use-the-O2-plugin-for-Obsidian/Pasted-image-20250102181248.png)

### 3. Configuration

Once the plugin is activated, you’ll need to adjust some settings:

- **Markdown folder**: Choose the folder where the Markdown files will be stored. I recommend keeping the folder name the same as the original.
- **Blog path**: Set the path where your blog is located. This is necessary so that the converted files can be moved to the `_posts` folder of your blog.

The settings should look like this:

![image](/assets/img/2025-01-02-How-to-use-the-O2-plugin-for-Obsidian/Pasted-image-20250102182647.png)
![image](/assets/img/2025-01-02-How-to-use-the-O2-plugin-for-Obsidian/Pasted-image-20250102182725.png)

### 4. Conversion command

If the blog path field is not filled in, the conversion command will not appear. To run the script that converts the Markdown files, follow these steps:

1. Press `Ctrl + P` to open the command palette.
2. Type `o2`, and the command will appear.
3. Press `Enter` to convert the files and move them to the `_posts` folder of your blog.

See the command in the image below:

![image](/assets/img/2025-01-02-How-to-use-the-O2-plugin-for-Obsidian/Pasted-image-20250102182415.png)

### 5. Final result

After running the command, the converted files will be in the `_posts` folder. The images and other elements of the converted Markdown will be organized into their respective folders. To publish the content on my blog, I only used Obsidian to write and the terminal to commit and push the changes.

## How did I discover this plugin?

While creating my blog, I wanted to centralize the entire process in Obsidian. By searching the community, I came across this plugin, which turned out to be a great find. The maintainer, Haril Song, has always been very friendly and helpful, clarifying all my doubts about the plugin.

I recommend following Haril on LinkedIn and GitHub and checking out his blog, where he shares events, books, and his opinions about the dev world. It’s amazing to exchange ideas with developers from around the globe. I believe that tools like this, which are open source, are essential for fostering innovation and new ideas in software development.

## My contribution to O2

While developing my blog, I noticed it would be helpful to store the converted files in a folder other than `_posts`. Reviewing the project’s issues, I found a discussion about this exact functionality. I decided to contribute, cloned the repository, implemented the new feature, conducted the necessary tests, and submitted a pull request.

Haril Song reviewed my contribution and approved the pull request. I was thrilled to contribute to a project that I use for my blog and that has been incredibly helpful.

![image](/assets/img/2025-01-02-How-to-use-the-O2-plugin-for-Obsidian/Pasted-image-20250102184732.png)

That’s my tip for today. Thank you for reading and...

Keep learning,  
**_Pedro_ ;)**
