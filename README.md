# xcresources

[![Twitter: @mrackwitz](https://img.shields.io/badge/contact-@mrackwitz-blue.svg?style=flat)](https://twitter.com/mrackwitz)

`xcresources` searches your Xcode project for resources and generates an index
as struct constants. So you will never have to reference a resource, without
knowing already at compile if it exists or not.

It includes **loose images**, **.bundles**, **.xcassets** and
even **.strings** in the index.

It gives you **code autocompletion** for resources, without the need of an
Xcode plugin and even for string keys.

Especially if your app is a bit more complex, this will greatly improve your
workflow. It ensures a better quality and gives you more safety.
You will see directly when a resource is missing, because you renamed it,
or you moved it around.

Furthermore it won't even bother you for trivial name changes like change
capitalization or converting name scheme from *train-case* or *snake_case* to
*camelCase* and vice-versa.

It will warn you in Xcode on build, if certain resources or string keys can't be
references, because their name contain invalid chars, duplicates in the
*camelCase* variant with another key, or would be equal to a protected compiler
key word.

The generated index could look like below:

```objc
const struct R {
    struct Images {
        /// doge.jpeg
        __unsafe_unretained NSString *doge;
    } Images;
    struct ImagesAssets {
        /// AppIcon
        __unsafe_unretained NSString *app;
        /// LaunchImage
        __unsafe_unretained NSString *launch;
        /// DefaultAvatar
        __unsafe_unretained NSString *defaultAvatar;
    } ImagesAssets;
    struct Strings {
        /// Alert title shown if a wrong password was entered.
        __unsafe_unretained NSString *errorTitleWrongPassword;
        /// Alert message shown if a wrong password was entered.
        __unsafe_unretained NSString *errorMessageWrongPassword;
    } Strings;
} R;
```


## Installation

Install the gem on your machine:

```bash
$ gem install xcresources
```

Use the automatic integration to add a build phase to your project,
by executing the following command:

```bash
$ xcresources install
```


## Usage

Reference your resources safely with the generated constants.

### xcassets Images

Assuming your xcassets bunlde is named `Images.xcassets`.  
`xcresources` supports multiple bundles in one project.

Instead of:

```objc
[UIImage imageNamed:@"PersonDefaultAvatar"]
```

Just write:

```objc
[UIImage imageNamed:R.ImagesAssets.personDefaultAvatar]
```


### Loose Images

Instead of:

```objc
[UIImage imageNamed:@"table_header_background_image"]
```

Just write:

```objc
[UIImage imageNamed:R.Images.tableHeaderBackgroundImage]
```


### Strings

Instead of:

```objc
NSLocalizedString(@"error_message_wrong_password", @"Message shown if a wrong password was entered.")
```

Just write:

```objc
NSLocalizedString(R.Strings.errorMessageWrongPassword, @"Message shown if a wrong password was entered.")
```
