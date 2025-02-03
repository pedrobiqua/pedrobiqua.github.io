---
layout: post
category: Blog
author: pedro
tags: [home_lab, umbrel_os]
title: "My Experience Using UmbrelOS"
math: false
mermaid: false
date: Sun Feb 02 2025 21:00:00 GMT-0300 (Horário Padrão de Brasília)
description: In this post, I will share my first experience using UmbrelOS on an old laptop.
---

One day, while driving back from my grandmother's house and talking to my dad, I found out that we had an old PC at home. Since I was looking to set up a home lab, I decided to repurpose this old laptop and turn it into a server.

While researching, I came across two self-hosting-friendly operating systems: [CasaOS](https://casaos.io/) and [UmbrelOS](https://umbrel.com/?country=BR). My choice wasn’t technical at all—I picked UmbrelOS simply because it has a more user-friendly interface and, in my opinion, looks better than CasaOS. The installation process was quite simple, following the instructions from the Umbrel repository. I installed the system on a USB drive.

![image](/assets/img/2025-02-03-Minha-experiencia-utilizando-o-UmbrelOS/Pasted-image-20250203142817.png){: width="300" height="200" }
_This USB drive has helped me a lot in college._

## Gitea

![image](/assets/img/2025-02-03-Minha-experiencia-utilizando-o-UmbrelOS/Pasted-image-20250203144522.png)
_Gitea App_

After installing it, I realized that UmbrelOS wipes and reformats the entire disk. I was able to access it through the browser, where I created my account and password. Then, I installed several apps, including Code-Server, Gitea, a file organizer, Jellyfin, Transmission, and Nextcloud.

I really liked Gitea because self-hosting my repositories is very useful. Most of my projects are on GitHub, but a large portion of them are college assignments and tests with frameworks and programming languages. Having a dedicated environment to store this "junk" is a great alternative. Many times, when I’m learning something new, I like to version my code so I can go back if needed. I’ve done this a lot, especially when I was learning my first Cython with C++ codes.

## NextCloud

![image](/assets/img/2025-02-03-Minha-experiencia-utilizando-o-UmbrelOS/Pasted-image-20250203144641.png)
_Nextcloud App_

Next, I tested Nextcloud and found it to be a great alternative to Google Drive and similar services. However, I don't fully trust it yet, since everything is stored on a single HDD. If the drive fails, I would lose all my files. Still, it could be a good option for storing family photos and videos, helping to free up space on Google Drive.

## Jellyfin

![image](/assets/img/2025-02-03-Minha-experiencia-utilizando-o-UmbrelOS/Pasted-image-20250203144732.png)
_Jellyfin App_

With Jellyfin, I was able to store my movies, which I ripped using my DVD drive. Yes, I still use DVDs and CDs, mainly to study Japanese and Chinese.

![image](/assets/img/2025-02-03-Minha-experiencia-utilizando-o-UmbrelOS/Pasted-image-20250203145305.png){: width="300" height="200" }
_My DVD and CD drive_

Since I like easy access to my media, having a server to stream content to my phone and other devices would be very convenient.

## An Unexpected Issue

During my tests, the laptop I was using as a server broke down. As a result, I couldn't explore UmbrelOS in depth. However, I’m already planning to build a new server, this time using boards like the Orange Pi and repurposing some old hard drives I have lying around.

## Reflection

Testing UmbrelOS was a great experience. I really enjoyed it, and it has definitely motivated me to build a home lab. I found the system practical and functional, and now I plan to set up a more robust server. I'll start with a simple solution and, in the future, look to improve it further.

**Keep learning,**
**_Pedro_ ;)**