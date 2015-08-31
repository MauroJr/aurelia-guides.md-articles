## Introduction

The purpose of the Aurelia-Guides project is to collect and organize all Aurelia related information **that is not included** in the [Aurelia official documentation](http://aurelia.io/docs.html).Since this is a dynamic definition, the following few paragraphs try to refine it, with the goal to collect as valuable information as possible, with the least amount of redundancy, overlaps with official documentation and maximum accessibility. This last attribute _maximum accessibility_ is the area where we expect to offer some **innovation**.

Initially Aurelia-Guides content belongs to two distinct categories:

#### 1.Large portions of text

 written in form of a blog or a tutorial.  This is the primary method for adding value to Aurelia-Guides repository and includes everything of interest on how to build an Aurelia application or Aurelia Plugin, using different development tools, different back-ends, various databases, interfacing third party API, etc..(_This definition is expected to be expanded as we develop this project_). The **[Authoring blogs / tutorials](#auth_blogs)** section that follows below provides the details how to do that.

#### 1.Code snippets
acquired by people answering questions in Gitter hosted **[Aurelia/Discuss][1]** chat room. The **[Adding snippets](#auth_snippets)** section that follows below provides the details how to do that


Each of these two categories has specific workflow assigned, which describes the process of contributing data from that category.

<!––nextpage––> 

## <a name="auth_blogs"></a>Authoring blogs / tutorials

This workflow is slightly more than trivial (say different from filling a form on this site), since the articles for Aurelia-Guides site **are maintained** in Github repository <https://github.com/aurelia-guides/aurelia-guides.md-articles> subsequently referred to as `Aurelia-Guides sources` and they **are rendered** at <http://blog.aurelia-guides.com> site. This separation of maintenance and rendering environments might be only temporary and is currently in place because of perceived difficulties related to use of **[Jekyll and Github-pages][2]**

The beginning of your request for contribution is well known to any Github user:

**Step 1** Clone the repository

**Step 2** Add your own article (probably starting with the article summary like **[this one][3]**:
 

>Testing is an integral part of any modern web application. A write-up on testing every aspect of Aurelia from A-Z would undeniably be super helpful for newcomers as well as helping expose users of Aurelia to various aspects (not limited to unit testing).

>A nicely broken up post on testing from ViewModels, to Custom Elements and Attributes. The various features like Behavior Instances, Containers and using methods like registerInstance, etc.

>**Dwayne Charrington** (Vheissu) is authoring this post.


**Step 3** Create the **[PR][4]** which will be processed by the site owner (@adriatic and @delebash initially)

There are a few volunteers already that will assess whether your article matches the Aurelia-Guides needs and will let you know whether to proceed with authoring process.

Once you signal that the article is finished one of the site owners will ensure that the article appears at Aurelia-Guides site.

At this early stage, given the number of very motivated early adopters compared to the number of articles already written, almost anything goes. If you have already written information of interest to others on your own blog site, please consider adding it here (bidirectionally linked). Check our **["Aurelia-Guides sources repository*][5]** to find out whether something you are considering to write about already exists (a very unlikely event :-) )

**Your active participation in this process is of critical importance to the whole concept of Aurelia-Guides** - there are several order of magnitude more Aurelia developers than Aurelia core team members and we are all in a great position to influence the success of Aurelia adoption, success that Aurelia deserves because of its unique forward looking architecture and incredibly talented and motivated development team.

Any question - please create an issue **[here][6]**

<!––nextpage––> 

## <a name="auth_snippets"></a>Adding code snippets


You will be adding code snippets to Aurelia Guides using the ScribeFire Snippet Manager plugin.

First credit goes to the great folks at [ScribeFire][9] who made the plugin!

To use ScribeFire, just click on the appropriate links to install the extension for you browser.

[Chrome][7]

[Opera][8]

*Note:* At this time it does not work in Firefox and I do not have a mac to test on [Safari][10] but if anyone wants to test on [Safari][10] and give us feedback that would be great.

### Setup and Usage instructions for the ScribeFire Snippet Manager.

_**Note:**  This is for the Chrome extension but should be the same for Opera and Safari if the Safari extension works._

**Step 1** Install plugin for [Chrome][7]

**Step 2** ScribeFire(Snippet Manager) will be added to Chrome's Extension bar in the upper right corner 
[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_00-45-38.png" alt="2015-08-29_00-45-38" width="40" height="31" class="alignnone size-full wp-image-283" />][11]

**Step 3** Click on the ScribeFire button to launch. Close the Welcome window, (you will only see it only  once). 

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-30-27-300x142.png" alt="2015-08-29_01-30-27" width="300" height="142" class="alignnone size-medium wp-image-290" />][12]

**Step 4** In the upper left corner to the right of Blog click on the link that says Add a New Blog 

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-31-12.png" alt="2015-08-29_01-31-12" width="299" height="64" class="alignnone size-full wp-image-291" />][13]

**Step 5** Type or paste http://collector.aurelia-guides.com/ into the URL box

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-37-09-300x199.png" alt="2015-08-29_01-37-09" width="300" height="199" class="alignnone size-medium wp-image-292" />][14]

**Step 6** Click next (Make sure you click the next button in the Url Dialog box before entering the username and password.

**Step 7** After clicking next you should be brought to the username and password box. Enter clipper for the username and aurelia for the password. All posts will use this common username and password.

In the future we are thinking of adding a custom field where you can type in your name if you want credit for the snippet.

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-41-07-300x198.png" alt="2015-08-29_01-41-07" width="300" height="198" class="alignnone size-medium wp-image-293" />][15]

**Step 8** Click Finish and in the upper left you should recieve a message that the blog was successfully added.

This completes the installation, next we will go over usage

### ScribFire Usage

First please click on Visual Editor link on the right side of the Post Content Title Bar in order to switch to the Markdown editor versus the HTML editor which can cause problems. Your settings will be maintained the next time you launch ScribeFire

Next add a Title and some Content, you can save this post for later if you don't want to publish right away by clicking on Save Progress in the lower right corner. To publish click Publish in the lower right corner next to Save Progess.

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-59-34-300x158.png" alt="2015-08-29_01-59-34" width="300" height="158" class="alignnone size-medium wp-image-296" />][16]

When you click Publish after success you will be presented with a dialog box allowing you to continue editing this post or start a new post. The contine editing button does not work but if you want to contine editing just close the dialog box and continue editing per normal then choose update post to push your changes.

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-03-41-300x198.png" alt="2015-08-29_02-03-41" width="300" height="198" class="alignnone size-medium wp-image-299" />][17]

ScribeFire remembers it's last state, so if you created a new post and published that post then closed ScribeFire, when you open it up again you will be on your last post in Edit mode verse Add New. There are two ways to get into Add New Post.

### To Add New/Edit exising Post

To Add:

1.  When you Publish a post and are presented with the dialog box for a successful publish just click on Start a New Post then close ScribeFire, as it remebers it's last state, when you open it up again you will be in Add New post mode.

2.  On the left side under Post you can start a new Post by clicking on the link that says Start a New Post.

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-19-50-300x102.png" alt="2015-08-29_02-19-50" width="300" height="102" class="alignnone size-medium wp-image-300" />][18]

To Edit:

1.  Under Post on the left side choose the post you want to edit from the dropdown box. If you choose to edit a post the information will be loaded into the Title and Content fields. Please do not post inapporpriate things, since everyone is under the same username you can edit any published post, but please be curtious and only edit someone's post if you need to correct it or add relevant information. It would be nice if you where to leave your name that you edited this post and why.

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-19-50-300x102.png" alt="2015-08-29_02-19-50" width="300" height="102" class="alignnone size-medium wp-image-300" />][18]

1.  Also on the left side are Catagories and Tags, please choose at least on option either a category, a tag or both. For now you may add new Categories and Tags.

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-38-53-300x124.png" alt="2015-08-29_02-38-53" width="300" height="124" class="alignnone size-medium wp-image-301" />][19]

To close ScribeFire just close it's browser tab.

Full picture of ScribeFire for your reference.

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-39-58-300x139.png" alt="2015-08-29_02-39-58" width="300" height="139" class="alignnone size-medium wp-image-302" />][20]

### Using ScribeFire with Gitter

You can either copy the text you want, open ScribeFire and paste it into the content area. Alternatively as a shortcut highlight the text you want, right click to get the context menu and choose ScribeFire then Blog Selected Text. Note this feature only works on the Gitter WebSite but not in the Gitter App. If you use the Gitter App you can open ScribeFire via your browser and then just copy and paste from the Gitter app to ScribeFire. Hopefully that will change as I here Node Webkit team is working on allowing Chrome Extensions into NW, if that happens then it should be easy to just import FireScribe into the Gitter App.

[<img src="http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-48-56-300x150.png" alt="2015-08-29_02-48-56" width="300" height="150" class="alignnone size-medium wp-image-306" />][21]

### Inserting Code

Currently we do not support the Github Flavored Markdown but just the regular Markdown no triple back ticks for code blocks :(. Instead for code blocks you must wrap your code in `<pre></pre>` tags like so.

`<pre>
function helloWorld(){
console.log('Hello World')
}
</pre>`

Which will actually look like

<pre>function helloWorld(){
console.log('Hello World')
}
</pre>

For inline code wrap in a back tick ` which will look like

Some inline `<div>I am here</div>` code

Note: With inline code WordPress seems to mess up if you don't have a carriage return between the text above your inline code and your inline code so space it out.

Please let us know if you find this tool usefull or if you have any issues with the instructions.

Thank you and happy coding :)

 [1]: https://gitter.im/Aurelia/Discuss
 [2]: https://help.github.com/articles/using-jekyll-with-pages/
 [3]: https://github.com/aurelia-guides/aurelia-guides.md-articles/blob/master/Testing-In-Aurelia-from-A-to-Z.md
 [4]: https://help.github.com/articles/using-pull-requests/
 [5]: https://github.com/aurelia-guides/aurelia-guides.md-articles
 [6]: https://github.com/aurelia-guides/aurelia-guides.md-articles/issues
 [7]: https://chrome.google.com/extensions/detail/elkkomimknapgodalnkjeddkjnjkfmfp
 [8]: https://addons.opera.com/addons/extensions/details/scribefire/
 [9]: http://www.scribefire.com/
 [10]: http://www.scribefire.com/scribefire-4.3.5.safariextz
 [11]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_00-45-38.png
 [12]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-30-27.png
 [13]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-31-12.png
 [14]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-37-09.png
 [15]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-41-07.png
 [16]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_01-59-34.png
 [17]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-03-41.png
 [18]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-19-50.png
 [19]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-38-53.png
 [20]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-39-58.png
 [21]: http://blog.aurelia-guides.com/wp-content/uploads/2015/08/2015-08-29_02-48-56.png