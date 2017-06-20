# LUSH Digital Android Coding Style

## Importing settings into Android Studio

### Importing

1. File -> Import Settings
2. Check all and press OK

*Please note: These settings are based on using Linux.*

### Known issues

If you are using a Macintosh, the font renders incorrectly. This can be fixed by:

1. Opening Android Studio Settings
2. Editors -> Colours & Fonts -> Font
3. Change Scheme to `Darcula`, instead of `MyDarcula`

## Coding Style

### Spaces or tabs?
Tabs.

### Curly Braces Placement
New line. Not shifted. All code throughout all projects should look the same and this a fundamental in making that happen.

### Java 7 & 8 or Kotlin?
Now that Java 8 is fully supported in the default Java toolchain, using Java 8 is fine and you shouldn't just be restricted to pre-8 features. Use of Kotlin is also fine now that it is first class citizen in the Android world but it is certainly preferred that a project be entirely in one language. For example, if the commerce app is written entirely in Java, then writing newer classes in Kotlin is not preferred - it's fine if you want to write libraries in Kotlin and add them to an all-Java project though.

If looking for guidance on a preference, I'd suggest starting all new projects in the Kotlin language. This is going to have a much longer lifecycle than Java (It's days are numbered now).

### Code Comments
Use of comments are your own judgement. Put yourself in the position of another developer in the team, would they understand the need for the method you just wrote? When building Fragment and Activity classes, having class documentation explaining where in the flow of the app the screen will appear is helpful but not mandatory. When creating a class which will be almost entirely business logic performing an important task (e.g. Service) then comments on the class and important methods are highly recommended; Use the TransactionQueueService of the POS project as an example of this.

### File Naming
#### Java/Kotlin File Naming

#### Resource File Naming
Outside of drawables and layouts, most resources will usually just be one file per resource type, making it easy to name, e.g. dimens.xml, colors.xml, strings.xml. The exceptions are in drawables and layouts where they must be named in the following fashion.

##### Drawables

- If the image file is for an icon it must be prefixed with 'ic'. e.g. ic_add.png.
- If the image is large and used to cover a large area then it should be prefixed with 'img'. e.g. img_splash.png.
- If the image is to be used as a background for an element such as a button, it should be prefixed with 'bg'. This usually applied to, but not limited to, XML drawables such as shape elements.

##### Layouts
Any layout file should have one of the following prefixes:

- 'view': Used for layouts that are not complete and only contain a part of a larger view. Typically used for layouts called using <include />.
- 'fragment': A layout file used by a fragment.
- 'activity': Layout file used by an Activity.
- 'dialog': Used in any form of dialog (AlertDialog, DialogFragment, etc.).
- 'item': Used for re-usable items in list. Most commonly used for RecyclerView.

### Open Sourcing
As a policy at LUSH, as much code as possible should be open-sourced. This should be considered at all stages of development and sensitive information such as API keys and comments containing sensitive business logic should be moved into a file not committed to git and loaded at compile time using gradle.

### Variable Naming Convention

#### Global Class Variables

#### Static Final Variables
The naming of private/public static final variables will depend on their use. For example, if it's being used to assign to a response to an Activity, the variable will be prefixed with ''RESPONSE_'. These are the currently considered prefixes:

- 'REQUEST': When requesting permissions or system resources.
- 'EXTRA': When saving or retrieving from Bundle
- 'RESPONSE': When requesting a response from an Activity or similar

#### Method-Scope Variables
Method-scope variables can be anything really. One-letter variables are not to be used unless in a for loop.

### Ordering methods in class
As a general rule, methods in a class will appear in this order:

 - Overridden methods
 - Abstract method declarations
 - Public methods
 - Protected methods
 - Private methods
 
Also note that where Fragment or Activity lifecycle methods are overridden, they should appear in the order in which they are called in the lifecycle (To the best of your knowledge, don't worry about being exact).

## Singletons?
Yes but only when you must. Singletons really shouldn't be overused because of their concurrency and leak potential but when there are uses that mean that you can only really use singletons to avoid excessive management of data then it's better to just keep things in memory.

## Project Strucure
The structure of the classes and packages in the project should be defined by it's features. This is obviously going to be driven by the purpose of the project so there's no strict rules around how it should be structured. As an example of structure, let's use the retail POS app. Some of it's key features are selling products, refunding products, gift cards, and manager functions. As a package structure it would look like the following:
-pos
	--model
	--activity
	--sales
		---fragment
		---adapter
		---holder
		---view
		---activity
	--refund
		---fragment
		---adapter
		---holder
	--giftcards
		---fragment
		---adapter
		---holder
		---model
-lib
	--factory
	--helper
	--manager
	
As you can see in the example above, each feature is then broken down into the classes that would then create a feature. So using the examples above,

- 'fragments' would contain all of the Fragment implementations
- 'activities' would contain all the Activity implementations
- 'adapter' would contain adapters for any RecyclerView or Spinner that it may be using to present data
- 'holder' for the view holder implementation for the RecyclerView it's using
- 'view' for any custom implementations of the View class
- 'listener' would contain simple Java callback interfaces used as callbacks in the observer/obversable paradigm.

The 'lib' package contains classes that fit into the standard Java paradigms like factory classes and singletons in the manager package.
