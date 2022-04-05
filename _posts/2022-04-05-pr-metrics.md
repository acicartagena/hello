---
layout: post
title:  PR Metrics
description: Quick glance on details and metrics on your Github PRs
date:   2022-04-05 01:12:35 +1000
image:  '/images/posts/pr-metrics.png'
tags:   [code reviews, prmetrics]
---
View detailed (but anonymous) Github Pull Request Metrics. The app anonymises the contributors of the repo to lessen the bias when viewing the data. 

Be able to see the time it takes from publishing a Pull Request to the first review comment. Measure the time in between the last commit and when the Pull Request is approved. Have a quick overview of the time in between approving a Pull Request to when it gets merged. 

PR Metrics offers a quick glance into your Github repositories pull requests. 

Scroll through the list of Pull Requests or be able to switch between different charts and tap to be able to see interesting points.

### Feedback
(If you have questions, concerns, issues, or feature suggestions, you can email me at hello@aci.codes)

### v1.0
- Shows repositories you have submitted a Pull Request or reviewed a Pull Request
- Currently only getting the last 50 commits, 10 reviews and 5 opinionated reviews for a given Pull Request
- Asks for `repo` scope on Github OAuth to be able to read your repository pull request information

### History
What started off as me exploring GithubAPIs to be able to graph the data into Google Sheets became an app.