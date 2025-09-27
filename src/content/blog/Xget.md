---
title: Xget
description: "本文介绍了一个用cloudflare部署的高质量库：Xget"
pubDate: 2025/09/27
heroImage: "Xget.png"
tags:
    - 工具
    - xget
    - 开发效率
---
# Xget
##### Xget：开发者的开源资源加速神器🚀

在全球化的开发环境中，访问 GitHub、npm、PyPI 等海外开源资源已成为日常。然而，对于中国大陆的开发者来说，网络瓶颈、访问失败、下载缓慢等问题却屡见不鲜。**Xget**正是为了解决这一痛点而生。

##### 什么是 Xget？

**Xget** 是一个高性能、安全、稳定的开源资源加速平台，支持 GitHub、GitLab、npm、PyPI、conda、Docker、Hugging Face 等数十个主流开发平台。它通过智能 URL 转换和边缘缓存技术，让开发者在国内也能享受丝滑的下载体验。

##### ✅ 极速访问 🔒 安全可靠
Xget 基于 Cloudflare 全球 CDN 网络，支持 HTTP/3 协议，响应速度低至毫秒级，真正实现“秒开”体验。采用 HTTPS 强制传输、路径长度限制、XSS 防护等多重安全机制，保障数据安全。

### Xget-tncrr.us.kg
Xget官方因为使用人数太多导致cloudflare的workers超额了，所以我根据存储库中的部署到cloudflare进行部署，只需在Xget Now中替换Xget链接为xget.tncrr.us.kg即可重新享受高速下载