## 1 Introduction
I like Apple. And I really like to develop native iOS Apps with Obj-C or now Swift, as it just feels right to me. But in the end you are standing there with a wonderful iOS App, for iOS phones and/or tablets and thats it. At this point you could be happy, but think about this:

**You are not targetingt about [80%](http://www.idc.com/prodserv/smartphone-os-market-share.jsp) of the market!**

And if you want to reach a greater audience either why you or your customer wants it, or because you don't want to miss the income from the millions of possible users, you will need another app. Now the rage begins, because you will have to deal with Java (urgh) and learn the Android SDK, or hire someone. Anyway, you will end with 2 codebases you have to maintain, which will be a pain in the ass over time.

To solve this problem, hybrid development was invented and slowly made it's way to the top. As there are still many prejudices and misunderstandings regarding those Frameworks, this article aims to show you *how* and *why* you should stick to the hybrid approach in your next mobile application project. 

### 1.1 Welcome to 2015
First of all, congratulations! We are in 2015 and this means you are way better of then 5 years ago, when hybrid development began to raise as a very promising area. The problem is, it was so shitty at that time, all the crappy apps have been burned into the minds of people which lead to preconceptions all around the globe.

Let's leave all those thoughts behind, open your mind and I promise you won't regret it.

### 1.2 Frameworks, Frameworks everywhere
It starts with the decision which framework to go with. They somehow sprout like mushrooms, and it might be hard to pick the right one. You could read infinite articles, consider your programming language background or analyse the cost and value of each. 

Or, you could just open your eyes and think for a moment, what might be the most stable, promising and free web framework? [AngularJS](https://angularjs.org/).

And which hybrid framework is free and gives developers all opportunities they need while having a huge fanbase? [Cordova](http://cordova.apache.org/).

Let's combine those two awesome frameworks and you get? [Ionic](http://ionicframework.com/)!

### 1.4 Why Ionic
Ionic combines AngularJS (JavaScript by the way) with HTML5+CSS and uses Cordova to access native device functions. Moreover it's free, the fanbase and support is growing every day and finaly the team behind Ionic is awesome. Just check out [there](http://ionicframework.com/creator/) [side](https://apps.ionic.io/landing/push) [projects](http://ngcordova.com/) [and](http://ionicons.com/) [you](http://ionic.io/) [know](http://ionicframework.com/present-ionic/) what I mean.

So all in all, Ionic offers great possibilities to build hybrid apps which not only look awesome, but which also behave as natural as a native app and rely on one shared codebase. And if you a scared of JavaScript, it's not as bad as you might think. Give it a chance!

The next parts of this article will highlight how Ionic Apps can replace most of what you daily use in iOS Development. We will see how to easily substitute well known components from native iOS development with HTML5 and JavaScript, how the structure looks and what you can achieve with the hyrbid approach.

## 2 Comparing native iOS with Ionic 
To show you the transition from iOS to Ionic we will go through the most important areas, however, if you already want to try Ionic I can recommend the [Ionic getting started guide](http://ionicframework.com/getting-started/).
### 2.1 Structure
When you start your Ionic project, you will find many files which might irritate you in the beginning. Remember how you started your fist xcode project? I guess that was a hell of file overload as well.

Let's take a short look at the config parts:
- **package.json** lists the used [NodeJS](https://nodejs.org/) modules
- **bower.json** lists the used [Bower](http://bower.io/) packages
- **config.xml** has all the properties for your created cordova project
- **gulpfile.js** describes [GulpJS](http://gulpjs.com/) build tasks

Those files are the base for your Ionic project. They are not very different to any other AngularJS application you might have seen. Additional you have some folders:

- **hooks/** Not that important in the beginning,contains scripts which run at specific points of the workflow.
- **plugins/** your installed cordova plugins
- **www/** this is where the magic happens!

Most of the time you will just work in the www/ folder, because your app's code is in there. The folder is just like a webproject, you could serve it with any server and see your app inside a normal browser. Almost ever you will start with the **index.html** or **app.js** inside that folder, which are like the backbone of your app.

### 2.2 Layout
As an iOS developer, you can either use the Storyboard/xibs to create the user interface, or you can jsut do it in the code. Either way, you have great options for using Autolayout to guarantee your app looks and behaves just as you wish on different screen sizes, although there are a only a bunch of sizes.

If you switch to Ionic, you will in general have all the layout in HTML files, which means you are best of with using relative sizes. The general markup looks like this:
```markup
<body ng-app="myApp">
  <ion-content>
   <ion-nav-view></ion-nav-view>
  </ion-content>
</body>
```
It's not very different to HTML, you might need to get used to some custom tags from Ionic and AngularJS which will simplify your development dramtically! For me, it's a lot easier to create the general layout fo my app inside HTML than with some xib file in Xcode. But you can decide for yourself whether you like it or not. Just remind  the hell on earth for a moment: *Xcode Constraints*.

Besides the HTML, you also have some JavaScript files (*please don't think of the JavaScript from some years ago*) which control your app and can change the views as well.

Ionic makes it so easy to deal with different screen sizes, it's almost fun to develop and see your app running so smooth on all kinds of devices.

### 2.3 Navigation
For now you have seen enough of the general stuff. Let's look at some code and see Ionic in action. This section aims to show you some core concepts, it is not meant to be read as a step-by-step tutorial. For things like that take a look at the [official Ionic Page](http://ionicframework.com/) or read on [my blog Devdactic](http://devdactic.com/).
#### States
The routing of pages happens through states in Ionic, which are configured for URLs. This means, you can specify different states, child states, abstract states and so on in your **app.js** like this, which will be loaded to your **index.html** inside the ionic-view:
```javascript
$stateProvider
  .state('tab', {
    url: "/tab",
    abstract: true,
    templateUrl: "templates/tabs.html"
  })

  .state('tab.dash', {
    url: '/dash',
    views: {
      'tab-dash': {
        templateUrl: 'templates/tab-dash.html',
        controller: 'DashCtrl'
      }
    }
  })
```
Additional you can already set the template file which belongs to a state and the regarding controller. In Xcode, the templates would be your xibs and the controllers the UIViewControllers of your app.

This state concept is sometimes tricky and might be hard to understand, but it's definitely one thing: A very good overview about all the possible states of your app! Something Apple tried to achieve with the storyboard, but I'm not sure how many people really use it all the time.

#### Tabbar
The tab bar is well known to every iOS developer, and with states and Ionic it's not hard to define it:
```markup
<ion-tabs class="tabs-positive">

  <ion-tab title="Status" icon-off="ion-ios-pulse" icon-on="ion-ios-pulse-strong" href="#/tab/dash">
    <ion-nav-view name="tab-dash"></ion-nav-view>
  </ion-tab>

</ion-tabs>
```
As you see, you can define all the things you need right inside your HTML. It might look a bit like magic at first, but when you start with Ionic you will get used to it. Furthermore, the whole view/templating/replacement philosophy comes in most parts from AngularJS, so if you are a bit familiar with that, thats a big point for you!

#### Navigation controller
To get a UINavgation controller you have to set some delegates and a bit of logic. With Ionic? Well, besides these few lines and setting the states and parent states of your app correct not very much! 
```markup
<body ng-app="myApp">
  <!-- The nav bar that will be updated-->
  <ion-nav-bar class="bar-positive">
  </ion-nav-bar>

  <!-- Where your views will be rendered -->
  <ion-nav-view>
  </ion-nav-view>
</body>

```
You get the navgation bar pretty much for free, you don't have to care about how the history works at this point. The big point here is, you could take care of that if you like to! Almost all of those elements can be accessed from your controllers by injecting the matching delegate:
```javascript
function MyCtrl($scope, $ionicNavBarDelegate) {
    // Do whatever the $ionicNavBarDelegate delegate offers 
}
```
The delegation pattern should be very familiar to you as an iOS developer I guess. So this is another option on how to send messages between your view and controllers.
#### Side menu
There are more cool layout features, for now let's take a last look at one which is well known as the Master-Detail pattern in iOS development. The side menu is a painless side menu which you can either pull in and out, or have it open on pad size devices all the time. The code would look just like this:
```markup
<ion-side-menus>
  <!-- Center content -->
  <ion-side-menu-content ng-controller="CenterContentController">
  </ion-side-menu-content>

  <!-- Left menu -->
  <ion-side-menu side="left" expose-aside-when="large">
  </ion-side-menu>
</ion-side-menus>
```
Thats everything you bascially need to get a sidemenu, pretty awesome right?

These were just some very simple rough examples of the code you need, but trust me, there a no hidden secrets, you will get a layout and a decent result ver, very fast.
### 2.4 Appearance 
The appearance of an app is the most important part in general. the iOS SDK offers many ways to get standard objects, which you have to customize most of the time if don't want your app to like like a boring normal app without style. 

Ionic offers some great way to get the same results in nearly no time, so read one for some example components.
#### Tableview
The UITableView is often used for displaying a lot of data. Setting up all the delegates, datasource and most of the time custom UITableRows can be a real pain. Just take a look at the next few lines for an Ionic tableview with 2 static rows:
```markup
  <div class="list">
  <a class="item item-icon-left" href="#">
    <i class="icon ion-mic-a"></i>
    Record album
    <span class="item-note">
      Grammy
    </span>
  </a>

  <a class="item item-icon-left" href="#">
    <i class="icon ion-person-stalker"></i>
    Friends
    <span class="badge badge-assertive">0</span>
  </a>
</div>
```
The result looks like this:

![TableView](http://i.imgur.com/Zt8lcGml.png)

Obviously static rows won't be used very often, but adding a controller to it which iterates of an array of objects is no problem with AngularJS at all!

#### AlertView
The UIAlertView is very handy for displaying errors or something similar to your users. Problem again here, it looks not very nice. The next few lines are all you need with Ionic..

```javascript
var alertPopup = $ionicPopup.alert({
     title: 'Looks good!',
     template: 'I hope you like Ionic'
   });
```
..to get a already good looking alert popup like this:
![TableView](http://i.imgur.com/1UnGmELl.png)
You can always change the appaerance of all your components, but we will come to this point later.
#### Gestures
Catching gesture input on your views is often mandatory to perform or prevent actions. If you think an hybrid framework is missing this feature, you are wrong (in case of Ionic!).

In my eyes, its even more easy than with native code, because this is all you need to catch swpie left event on something:
```markup
<button on-swipe-left="onSwipeLeft()" class="button">Swipe me left</button>
```
The same *directive* can also be applied to other elements like your content or whatever you like. Remember that you are running your app in a webview, and you still have all those native functions that easy!
#### Styling/CSS 
One of the biggest benefits is how fast you can style your complete app. When using buttons, navbars or other controls you can take predefined Ionic classes which can be great, or you can simply override those elements to have your app completely redesigned (regarding colour and CSS elements you can influence) in seconds!

As the team at Ionic is always working on solutions for problems like this, they already made a tool to create your custom stlye: [Ionic theme editor](http://ionic-theme-editor.herokuapp.com/) Hopefully, this editor will soon be also available inside the Ionic creator tool.

Anyway, if you don't like all that, you can still make your complete own design and apply it to your app. 

### 2.5 Pitfalls
Of course there are problems, but you will encouter problems everywhere. 

Ionic 1.0 is still not released, an there are open bugs. But if you work with it and follow their speed of development, you can be very sure that they are after every bug, plus trying to give more options to developers every day. If you still feel the need to talk to them, you can always reach them on twitter and they will help you out.

If you are a programming language fanatic, you might find JavaScript ugly as hell. It might not be the best language out at the moment, but with ECMAScript 6 in the near future, I believe the tides will turn very much. The well known classes concept will make its way to JavaScript, and the code will look much cleaner.

If you don't like AngularJS for whatever reason, you might also have a problem with Ionic as they work so strong together. In that case, I can only recommend you to think about AngularJS again, or if you still don't like it to wait for React Native.

Although we are in 2015, hybrid apps *can't* be native apps. Running in a webview always limitates your behaviour and feeling a bit, but I am damn sure you won't see the difference most of the time, and pretty sure you are using hybrid apps and don't recognize it. If you are planning a 3D game or something with heavy graphics, I might recommend you more to [Unity3D](http://unity3d.com/5), but for most of all apps out there Ionic could definitely be the way to go.

## 3 Building your app
When it finaly comes to building your app for distribution, Ionic comes with some tools which makes life a lot easier. 

First of all, the [Ionic CLI](http://ionicframework.com/docs/cli/) is great for the complete workflow of your app. Starting projects, adding cordova plugins, running and testing your app just works like you would expect it to do.

> If you are looking for a complete CLI overview, take a look at my [Ionic Cheatshet](http://devdactic.com/ionic-cheatsheet/)

I might have mentioned they are realling trying to solve problems. Take this for another example: [Automating Icons and Splash Screens](http://ionicframework.com/blog/automating-icons-and-splash-screens/)
Creating Icons and Splashscreens for your app is such an annyoing business, but they just solve this problem so you create one image and Ionic takes care of the rest.

When everythings done, you can finally build your apps again with the CLI with your preferred options and platform:

```bash
ionic package [debug, release] [android, ios]
```

The team has designed the complete workflow from starting an app to building it, and they are even working on something which allows you to share your apps with friends without any profile errors: [The Ionic view app](http://ionicframework.com/blog/view-app-is-alive/)

Of course, you can also open the created Xcode Project after building it from the command line, but it's just nice to stay in one environment when developing something.

## 4 Conclusion and outlook
I still like building native iOS Apps. But more and more, I tend to just make it hybrid the first time. It just feels like any other app in most cases, and in the end you have an app for 2 platforms and 1 codebase. The results are astonishing, and the moment you have the same app on your Android and iOS device without  going through any real Platform specific struggles is amazing.

Ionic is still not released in version 1.0, but the current status, the speed of development and the expanding fanbase on the Internet is a very good sign for a Framework, which could bring us a lot of fun in the next years.

Some of you will still hate hybrid frameworks, saying it will never feel like a native app. Ok you fools, go home. We're in 2015 and Ionic is here. 

