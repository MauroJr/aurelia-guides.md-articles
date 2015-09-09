**Aurelia-Guides** is a collection of documents written by a team of Aurelia Enhusiasts, consisting mostly from Aurelia early adopters and a few members of Aurelia core development team. The documents in **[Aurelia-Guides](http://blog.aurelia-guides.com/category/general-information/)** live &quot;independent life&quot; from **[Aurelia&#39;s official documentation set](http://aurelia.io/docs.html)**, it is expected that some (or more) of Aurelia-Guides documents will find their way to become official (_can this be perceived as the motivation to create world class contributions to this project :-) ?_)

* * *

## Aurelia-Guides tasks

The purpose of the Aurelia-Guides project is to collect and organize all Aurelia related information **that is not included** in the [Aurelia official documentation](http://aurelia.io/docs.html). Since this is a dynamic definition, the following few paragraphs try to refine it, with the goal to collect as valuable information as possible, with the least amount of redundancy, overlaps with official documentation and maximum accessibility. This last attribute _maximum accessibility_ is the area where we expect to offer some **innovation**, introduced [here](https://github.com/aurelia-guides/aurelia-guides.github.io/wiki/Data-Collection-and-Organization-Process#code--data-snippets).

### What to collect

Since this official documentation consists of just few initial pages, it is difficult to define the scope for Aurelia-Guides content. Here are the two main categories, (this list may grow as the data aggregation process advances)

##### Blog posts

Everything of interest on how to build an Aurelia application or Aurelia Plugin, using different development tools, different back-ends, various databases, interfacing third party API, etc..(_This definition is expected to be expanded as we develop this project_)

##### Code/Data Snippets

Any code snippet that can help others while building or testing apps / plugins. Note that most of such snippets appear (and get subsequently lost) in [Aurelia/Discuss chat room](https://gitter.im/Aurelia/Discuss). The term **Code Snippet** is indeed too narrow as, this category should include all information (like a reference to some resource of interest, brief &quot;how-to&quot; instructions) that the consumer of this information wants to make available for others at a later time. The best way to understand the value of the code snippets in the context of Aurelia-Guides,  is to realize that code snippets are generated in a situations when the existing documentation is unclear or insufficient - or both.


* * *

### How to collect

##### Blog posts

In order to ensure that **Blog posts** are of interest to many, and cover all areas of interest, without too much overlap, I propose the following process for each author of the post:

*   Create the entry in the **[issues section](https://github.com/aurelia-guides/aurelia-guides.md-articles/issues)** and give it the name of the article that you want to write and prepend the name with `Blog post proposal:` (this prepended string will later help filtering blog post proposals from other issues that are maintained in the same Github list). Use the Comments section of this issue to explain more details about the post you want to write
*   Someone from the set of editors (humans, not a piece of software) will regularly scan this issues section and ensure that the proposal is &quot;in line&quot; with the expectations we have about the content of this site and state his / her approval in that Comments Section.
*   All (approved) blog proposal issues will appear on the [Zenhub board](https://github.com/aurelia-guides/aurelia-guides.md-articles/issues#boards?repos=40382874) where the author can use the available &quot;agile&quot; tools to coordinate the subsequent life of this blog post.*   When you are finished with the first draft of your article, please remove the string `Blog post proposal:`, and update the status of your work at [Zenhub board](https://github.com/aurelia-guides/aurelia-guides.md-articles/issues#boards?repos=40382874).

**Note**: this process may appear over-designed for the creation of 4 blog posts by two authors; I expect this not to be the case and we might have thousands of posts by hundreds of authors - and then such workflow may even appear to unconstrained. However, we can always strengthen it as we have all tools available that are used in a more difficult environment (software development management). Until we reach first thousand articles however, please feel free to simply add your own article in **[https://github.com/aurelia-guides/aurelia-guides.md-articles](https://github.com/aurelia-guides/aurelia-guides.md-articles)** collection once you verify that that a similar article doe not yet exist.

##### Code / Data Snippets

As mentioned before this is a more involved process that requires more instant work from the &quot;benefactors&quot; of discussions in [Aurelia/Discuss](https://gitter.im/Aurelia/Discuss) chat room. I would like to create some relatively simple Aurelia application - [Snippet Manager](https://github.com/aurelia-guides/aurelia-guides.github.io/issues/4) that can be used as the intermediary (copy from Aurelia/Discuss chat room and paste into Snippet Manager) **in the context of using** Aurelia/Discuss chat room. Snippet Manager (which will likely have to be a Github app) will then persist these snippets together with the metadata created in the copy / paste action.

Until such utility application becomes available - please create your own snippet as an issue **[here](https://github.com/aurelia-guides/aurelia-guides.md-articles/issues)** using **[this snippet](https://github.com/aurelia-guides/aurelia-guides.md-articles/issues/20)** as a template

Clearly, we need to offer an innovative process for searching and rendering such huge collection of data, starting with the automatic creation of the before mentioned metadata (to insure proper categorization and search attributes).

* * *

#### Publishing posts

All finished posts (this is determined by the blog post status on the [Zenhub board](https://github.com/aurelia-guides/aurelia-guides.md-articles/issues#boards?repos=40382874)) will be published at  [//http:blog.aurelia-guides.com](http://blog.aurelia-guides.com/) 

**Note**: Initially, I assumed to use [Github pages](https://pages.github.com/) and Github hosted instance of [Jekyll](http://jekyllrb.com/). This turns to be a bad idea after two weeks of hard work, tens of interactions with Github support - and the finished &quot;product&quot; looked and behave unacceptable. So, this blog is a WordPress application hosted at [http://www.one.com](http://www.one.com/en/)
