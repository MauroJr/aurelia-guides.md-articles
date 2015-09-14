## Introduction

This blog is a series of posts explaining the use of [Identity Server - with STS](https://www.dotnetfoundation.org/thinktectureidentityserver) , [Stormpath](https://stormpath.com/) and [Auth0](https://auth0.com/) as "Account Management PaaS" providers -- from the viewpoint of the Aurelia Application Developer. So, the material presented here does not attempt to define Aurelia Framework security abstraction component, but rather practical examples of using these three services

The above paragraph does not implicate how Aurelia Framework security abstraction component, but rather that we are starting with the bottom up approach creating the two initial Aurelia SDKs:

1. [aurelia-stormpath-sdk](https://github.com/aurelia-guides/aurelia-stormpath-sdk)
2. [aurelia-auth0-sdk](https://github.com/aurelia-guides/aurelia-auth0-sdk)

to be the first two components to be further abstracted as Aurelia Plugin

Unlike popular opinion, a typical "security services platform" does not only provide Authentication and Authorization services - it provides the complete User Management API - secure user infrastructure, from self-registration to single sign-on to token authentication. Such service is often referred to as **Identity As A Service** and a typical consumer of such services are web applications (as well as smart device applications) that have high demands on security, like health care patient portals or care management services - as well as a whole slew of security sensitive LOB ([Line Of Business](https://en.wikipedia.org/wiki/Line_of_business)) applications 

**Note** Since the expected customers for this Aurelia Component are mostly large businesses - the fact that the Security Providers being presented here are **not only** Open Source vendors, but also offer their services for a fee is indeed a benfit rather than a downside. 

----------
## Identity as a service / Account Managements PaaS service

To provide the proper terminology for this article, I will quote sections from the [Stormpath Datasheet](https://stormpath.com/resources/datasheet/) document.

In addition to authenticating users with a single call, Stormpath handles authorization, access control, password security, group management, and security workflows like user registration, email account verification and password resets.

A highly-available API built in an advanced cloud, Stormpath can be deployed privately or on-premise. Developers can use the API for free.

![](http://i.imgur.com/1GncCLY.png)

### A few more details
- Stormpath supports creation and storage of any number of user accounts. Assign your users to groups or associate entire user stores with one or many applications.

- There is no cap on the number of accounts you can add or the number of directories you can create, and we don’t charge per user. For one monthly subscription, your user management can be as complex or as simple as you need it to be, and all of it is accessible and manageable via both the API and our admin console.

- Stormpath can allow your users to log into all of your applications using the same credentials by connecting multiple applications to shared directories. No matter how many user directories you have, you can configure Stormpath to allow your application to see all your directories as a single user store. In addition to creating a unified user-experience, centralized authentication makes provisioning, disabling, and managing a user simple for admins.

- Automated password reset, account registration, and verification workflows boost the security of your application. With Stormpath, they come standard. Ensure passwords are reset in a secure way and verify new user accounts without a single line of code. You can also customize workflow emails with your own branded HTML. Stormpath operates behind the scenes so your users only see your application and your brand.

- Stormpath supports role based access control through the ‘group’ resource. Simply assign an account to the appropriate group(s) via our API or admin console. You can then design privileges in your application around specific roles such as users and admins.

- With Stormpath, your applications have full access to all of your group data, but you don’t have to build out and maintain custom data models or management logic. Stormpath can automatically limit who can log into your applications based on their directory or group memberships. Stormpath also helps you prioritize those login sources with a simple drag and drop interface in our admin console.

- Stormpath takes password security very seriously: we use SHA-512 and HMAC algorithms with large, secure, randomly generated salts. We add computational complexity to the hashing process to make it cost prohibitive for an attacker to breach even a single password.

- We also use other techniques, like authenticating requests with HMAC digests and advanced key derivation algorithms. It would effectively take an enormous amount of computing power to crack even a single Stormpath-secured password.

- Additionally, Stormpath helps encourage strong password security for your own users with built-in enforcement options like minimum password length and required special characters.

- We use advanced authorization with every request to provide full end-to-end data protection and ensure your data is never tampered with. We also carefully maintain data security in database maintenance processes, such as backups.

- Highly available, clustered data store with double or triple redundancy
- Low latency, multi-zone infrastructure on Amazon Web Services

### One very important detail, now

Most of the time Aurelia (front end) applications are perceived as a SPA-type applications (also called "untrusted clients" because people can easily alter or inject javascript code on a page through the developer console, so we do not want to embed sensitive information like secret keys or passwords in these types of clients. This "fear" leads to the concept of **"token based authentication"** - quite eloquently **[described here](http://docs.stormpath.com/guides/token-management/)**.

This very important detail mentioned in the header of this section is that Stormpath **[fully supports token based authentication](http://docs.stormpath.com/guides/token-management/#how-to-use-stormpath-for-token-based-authentication)** - meaning that a part of the service is the Security Token Server aka **[STS](https://msdn.microsoft.com/en-us/library/ee804740.aspx)** 







