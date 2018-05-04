# Project 7 - WordPress Pentesting

Time spent: **5** hours spent in total

> Objective: Find, analyze, recreate, and document **three vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. Unauthenticated Stored Cross-Site Scripting
  - [ ] Summary: An authenticated attacker can inject JavaScript in WordPress comments. This script is triggered when the comment is viewed.
    - Vulnerability types: Cross-Site Scripting (XSS)
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [ ] GIF Walkthrough: <img src="https://imgur.com/meljHFM.gif" width="800">
  - [ ] Steps to recreate: As an unauthenticated user to a WordPress website, reply (comment) on a post with an HTML anchor tag with a title attribute.     Inside the attribute quotes, add a JavaScript event handler along with some dummy text that must be at least 64KB long. The reason for the long         text is that when it is inserted into the database, it will be truncated. The truncation results in a malformed HTML element being generated on the page. After the comment has been submitted and the post viewed again, the JavaScript code will be executed resulting in an XSS attack.
  - [ ] Affected source code: N/A

2. Authenticated Stored Cross-Site Scripting
  - [ ] Summary: WordPress versions 4.2.2 and earlier are affected by a cross-site scripting vulnerability, which could allow users with the Contributor or Author role to compromise a site.
    - Vulnerability types: Cross-Site Scripting (XSS)
    - Tested in version: 4.2
    - Fixed in version: 4.2.3
  - [ ] GIF Walkthrough: <img src="https://imgur.com/R8Zvyxp" width="800">
  - [ ] Steps to recreate: An attacker would first log in with an account that has privileges of a Contributor or Author role. Then the attacker would attempt to create a new post on the site. The important key is for the attacker to use the HTML editor to create the post instead of the Visual Editor. The attacker would insert someting like `<a href="[caption code=">]</a><a title=" onmouseover=alert('test')  ">link</a>`. That HTML snippet would be processed and manipulated into `<a href="</a><a title=" onmouseover=alert('test')  ">link</a>` because the original snippet contained a WordPress shortcode. A shortcode is a technique for embedding a snippet of PHP code into the body of a page or other content item. As a result, when a viewer views the post, they see a link that doesn't really point to anything and when they hover their mouse over it, a XSS attack would be triggered.
  - [ ] Affected source code: N/A

3. Content Injection Vulnerability
  - [ ] Summary: This vulnerability allows an unauthenticated user to modify the content of any post or page within a WordPress site. One of the REST endpoints allows access (via the API) to view, edit, delete and create posts. Within this particular endpoint, a subtle bug allows visitors to edit any post on the site.
    - Vulnerability types: Privilege Escalation/Content Injection
    - Tested in version: 4.7
    - Fixed in version: 4.7.2
  - [ ] GIF Walkthrough: <img src="https://imgur.com/zueys1G" width="800">
  - [ ] Steps to recreate: First a user will view a post on a WordPress site. Through this vulnerability, a user will be able to duplicate a post just by appending alphanumeric characters the current post's URL and making a GET request to it. Interesting enough, the WordPress administrator would never know that the user created the duplicate post because it won't show up on their Posts dashboard.
  - [ ] Affected source code: N/A

## Assets

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.