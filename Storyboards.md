Introduction
Welcome to my first blog post! In this blog, I’ll be writing down my opinions about contentious issues in the iOS community. The first topic is about the eternal battle of using storyboards, xibs, and/or programmatic layouts. For the purposes of this discussion, 
Small Projects
I would define a small app as one having most of the following:
Eight or less viewcontrollers
One or two viewcontrollers for login
One navigation controller or tab bar controller
Five or six viewcontrollers for content post-login
Mostly static layouts (i.e., subviews not being added/removed/rearranged).
Little to no custom UI components (e.g., carousels)
No foreseeable large or frequent updates to UI.
1-3 Developers
3 months or less to complete the UI

For small apps, I would recommend storyboards for their high startup speed and readability.
Startup Speed
At least for me, it would be much faster to set up the layouts for a screen through Storyboard or a nib than it would be through code. Adding views into storyboard and setting up constraints between those views is a matter of a couple keystrokes and clicks. Furthermore, what you design in Storyboard usually reflects what you will see at runtime. Since Storyboard serves as preview, I could wait until I completely finish a screen before building and running the app to confirm the design at run-time. 

By comparison, if I were building a screen using nibs, I’d likely have to build and run the app several times to double-check my work. While you can design an entire viewcontroller in one nib file, unless that viewcontroller will be reused elsewhere, I’d much rather just create a Storyboard with the viewcontroller because nibs are more limited (e.g., no static table view cells, can only contain one view controller).

Finally, unless the view were very simple, I would not recommend designing it solely in code. Unless very well-organized, defining UI layouts in code can quickly create spaghetti code. At least for me, Swift’s imperative style of declaring UI is not an intuitive way to visualize a screen. With complex layouts, this spaghetti code can quickly lead to re-running the app often to verify the result. Whereas setting up a view’s properties in Storyboard might take just a few clicks, setting up each property through code might take a line of code per property. As you can imagine, the lines of code rack up very quickly, so I highly do not recommend designing an entire view through code. 

I have seen people set up views more quickly through code than through Storyboard (youtube link), but it required having a prepared toolkit of extension methods and custom UI classes. While these toolkits can be adopted to most apps since a lot of apps share the same basic layouts, not everyone has built one of these toolkits for themselves. I don’t have a toolkit of convenience methods and classes myself, so I’d need to build that toolkit first (which would take a significant amount of time) before even starting to build the app. Of course, for those who do have such tools, it might be just as easy for them to set up a small app through just code as it would in Storyboard.

Some words of caution with storyboards, however. I would recommend using multiple storyboards even for a small iOS app because, in my experience, numerous issues can happen in a storyboard that has even just one or two viewcontrollers. Storyboards are very fragile in that they can take a couple of seconds to load if there are too many view controllers or the layout for a single view controller is very complex (i.e., many ui elements, or complex relationships between elements). Further, it can be very difficult to resolve source control conflicts in Storyboard files since they can be hundreds of lines of incomprehensible xml. While source control conflicts are much less likely in a small project, I would still recommend using several storyboards as a precautionary measure.
Readability
If your views are relatively static, storyboards are a great resource for visualizing them at a glance. While a developer might need to read around 100 lines of code to understand the layout of a view, it could take just a few seconds to look at a storyboard and get a sense of the layout. Moreover, if there are multiple view controllers in a storyboard, a new developer can quickly understand the user flow in a particular of the app. For me, storyboards are great for small projects because I could temporarily stop working on an app and pick it back up later fairly quickly because I only need to look at the storyboard(s) to understand where the app was last. 
Large Project
I would define a large project as having most of the following:
An enterprise-level app
10+ view controllers
Dynamic views
4+ developers
4+ months to complete UI
Regular releases and updates to UI
Individual
I would be careful about this classification unless you are absolutely sure that your app will only ever have one or two developers working on it. If the app becomes popular and marketable, the team size can easily grow to be more than 3 developers. 

I would not recommend using only Storyboards for individual, large projects. While Storyboards are great for kickstarting a project and designing simple and/or static views, the time lost from not having reusable views is not worth it for a long-term project. 

I would recommend some combination of nibs with either Storyboards or code for an individual, large project. In this section, I will sometimes use the term “xib”, but this term is synonymous with “nib”. Personally, I would choose nibs with code because of three reasons:
Creating highly dynamic views is more straightforward
Easier unit testing due to control over viewcontroller lifecycle
Fragility of storyboards even in individual projects

Dynamic Views
When using storyboard, any views placed in the interface builder will be initialized at runtime. This can be a little problematic for views you may want to show or hide at runtime (e.g., empty/error states). Instead of removing/hiding the views you’ve defined in Storyboard in order to show these empty/error states. Building views through code allows you to decide which views even get initialized at run-time. 
Unit Testing
Along the same logic as dynamic views, a Storyboard-less app can give you more control over the lifecycle of viewcontrollers. Instead of allowing Storyboard to initialize your views for you, you can now define your own initializers/constructors, allowing for easier dependency injection of services and thus easier unit testing. 
Fragility of Storyboards
Even in a 1-3 person team, merge conflicts can occur. While likely less problematic than in a large team, merge conflicts in storyboards can be nasty to resolve. When the iOS team at 1904labs was still 3 people, we had storyboards that would occasionally fail to render either because of some partially failed merge conflicts or because the layouts were too complex. Even in our small team of 3 people, we faced this issue and, since the Storyboard file sometimes fails to render, we no longer have any of the benefits of Storyboards in visualizing the layout of that particular view.
Team
In a team setting, I recommend starting the project only with xibs and code, if possible. In practice, I realize that most people are comfortable working with storyboard, but not everyone is comfortable creating views only with xibs and code. 
