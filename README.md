# Flack
A Flutter stack. Flack.

## About
I develop Flutter apps, and have enjoyed using a number of packages together. This is my "starter kit" for the work I do, to help get into building and releasing functional, online/offline capable, deep linking, notification enabled, testable, extensible, and scalable apps quicker. 

Since there's really nothing in here that I've built myself, just standing on the shoulders of giants, I'm making it publically available in case anyone else wants to use it. 

I will also be maintaining a Wiki, which will have some poignant reminders and guides for both myself, and anyone ho things "how does that fit together again?" Who knows. If people find this useful, I might get someone way better at programming than me help to make our jobs even easier. I'm no genius. I'm no Leetcode high-score holder. But I make stuff that's used commercially. I make stuff that hopefully is usable and useful. 

## The Flack "Pattern"
There are a lot of patterns. Clean. MVC. MVVM. Hexagonal. Layered. Google "should I use clean architecture?" and you will often find, having risen to the top via very real internet points, "why don't you tell us more about what you're trying to achieve first?". There's not one pattern for all. Some may swear by one, some may swear at some. I borrow terms from various architectures that I've found tend to work well with Flutter specifically. 

This may sound a little holier-than-now, but at the core of it, it comes from the reality of my needing to build applications with a small/lack-of-a team:
**I use a pattern that helps me build and maintain apps, will protect my future self, and allows me to work efficiently and multi-task.**

So, I borrow, thief, mangle, steal, use, and HOPE that I've ended up with:
- Well documented, and self documented code.
- Single responsibilty, reusable methods and Widgets, wherever practical.
- Separated, loosely coupled architecture:
  - This is a non-negotiable. 
  - **Presentation**
    - It's there to look pretty, and provide accessibility. It's the human-machine interface.
    - The UI interacts with the application's "core" or "domain" **Providers**, to retrieve and/or submit **Entities**. 
    - If you had two UI's built, you should be able to drag-and-drop the "presentation folder" of one UI, onto the other, press build, and it works first time. 
    - The UI may have it's own "state management" layer, like **Forms** (viewmodels), its own validation, but this is ONLY for presentation. It MUST defer authority and final decisions to the **Core** layer. 
    - It must know how to display and deal with any **Exceptions** thrown from the core layer. 
    - It provides the **Router** for the application. Of course, one UI may have totally different routing requirements from another - e.g. mobile, vs tablet, vs desktop. 
    - The router can and should make use of **Guards** in the core layer. We should avoid embarrassing "can't load data because I asked for something I wasn't allowed before checking if I was" exceptions. 
    - The presentation layer *should*, whenever possible, use **Entities** directly from the core layer. In certain cases, this isn't practical, so there may be the "viewmodel" layer in between. But nothing in the core layer should be dependent on the UI. 
  - **Core**
    - It's the beating heart of your application. It's a computer before you've plugged in a screen, input devices, and a network cable. 
    - It provides what the presentation layer can show (dishing out **Entities** via **Providers**), and 
    - What the data layer should provide (**Repositories** and **Entities**).
    - The litmus test of success here is: 
      - Build the front-end and core layers of the application on a SINGLE MOCK JSON DATA SOURCE before implementing ANY remote API access, or even internal data persistence. Obviously it may be helpful, if it's available, to use a similar structure to an API you might be accessing. But not necessarily. 
  - **Data**
    - The data layer is the polyglot data translator service.
    - The data layer handles data manipulation and transformation to/from data storage services, either local or remote. 
    - The data layer handles connectivity issues gracefully.
    - The data layer does NOT handle data validation. Don't shoot the messenger.
    - The data layer speaks many language **Models**, and translates them into a common **Entity** language. 
    - The data layer looks at the **Repositories** in the Core, and **Impl**ements them. 
    - The data layer 

### Information Flow
At the 'core' of it here are the three laws of Flack:
- **All data flows into and out of the core layer**
- Data **never** flows between the presentation and data layers.

### Exception and Error Handling
Handling of 

## The Stack
I use a number of open-sourced packages that I've found work well together, and appeal to my style of coding. 

### Built-in
Some things I've provided as more a boilerplate for typical tasks that Flutter doesn't necessarily provide an opinionated way of doing, such as:
- Themeing system
- Color scheme system
- Font themeing
- In-app messaging with snack messages and persistent top message bars
- Routes for displaying modal bottom sheets and general pop-up modals

### Flutter
If you're here, you probably want to build apps using it. 

### RPS
Run Pubspec Script. Does what it says on the box. Helps with build-runner etc. 

### Build Runner
For code generation used in:
- Drift
- Riverpod
- JsonSerializable

Love it or hate it, Dart does not have static metaprogramming. Honestly if it did, I'd probably say "wow that's a stupid name" and move on. They talked about it, but they dropped official development. They're now focussing on developing better and more efficient build-tooling and code generation systems in Flutter itself.

What the hell is code generation? 

You've built a beautiful **Entity** class, with all the properies of the data that you need to display and process. `name` as a `String`, `dob` as a `DateTime`, `location_lat` as `double` etc. Now, you need, because of reasons, to convert it to JSON. You could write some `toJSON` method on your class. Perhaps even create a `mixin` called `JsonSerializable` or something, which gives you that method you can re-use. But hang on, Dart doesn't really have class introspection/reflection to access the structure of a Class. Ok there's a package for that called Reflectable. Hang on... That requires code generation to use... Hmm... Maybe someone has already done this serializable thing, surely it's a common use-case. 

So, what you COULD do, is add `@JSONSerializable` before your class definition, add the required `part some_serializable_class.g.dart` before that, start typing `toJSON` somewhere in your file and you'll get a code snippet for the `@override` and

### Drift
Your friendly local database package. It's not a full ORM, but by gosh, it's easier than programming your own SQLite interface from scratch. 

### Firebase
Firebase makes life VERY easy for us to set up, for FREE I might add:
- Remote configuration (Firebase Remote Config)
- Push notifications (Firebase Cloud Messaging)
- Crash analysis and statistics (Crashlytics)

### Flutter Secure Storage
Allows storage to secure device storage channels for more sensitive information such as access tokens. Where that is exactly depends on the target system. 

### Flutter Launcher Icons
Make generating all those crazy icon files much easier, from just one reference. 

### Flutter native splash
Make generating that opening screen much easier. 

### Riverpod
State management solution. Provides the communication layer between presentation and core layers. Used in the presentation layer to provide the global scaffold messaging access, current theme, user preferences etc. 

### Auto Route
The application router. 
#### Why this one? 

#### Alternatives
Go Router
