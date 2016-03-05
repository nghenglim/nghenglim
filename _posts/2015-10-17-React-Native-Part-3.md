---
layout: post
title: React Native Part 3
category: programming
tags: [React-native, iOS]
---

![React Native]({{ site.baseurl }}/images/2015100300.png "React Native")

In react native AwesomeProject example, it gets bundle files with 2 options:

1. Load from development server
2. Load from pre-bundled file on disk

### Hybrid options?

The react native default options looks good, but not good enough.

We would like it to load from development server asynchronously, and load from pre-bundled file on disk when the new bundled file is not ready yet.

Good news - with some enhance on the AppDelegate.m file that come with the AwesomeProject, it can be archieved!

### Coding

[View AppDelegate.m at Github](https://gist.github.com/nghenglim/46391331d443165d9d53)

First declare the variable, and set the filepath default store and get from the document directory.

~~~ c
NSArray   *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
NSString  *documentsDirectory = [paths objectAtIndex:0];
NSString  *filePath = [NSString stringWithFormat:@"%@/%@", documentsDirectory,@"index.ios.bundle"];
~~~ 

Under OPTION 2, asynchronously download file from server. Detect if the file exist in document directory, if the new bundle file exist, load from the document directory. Else, load from the pre-bundled file on the disk:

~~~ c
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
  NSURL  *url = [NSURL URLWithString:@"http://localhost:8081/index.ios.bundle?platform=ios&dev=true"];
  NSData *urlData = [NSData dataWithContentsOfURL:url];
  if ( urlData )
  {
    //saving is done on main thread
    dispatch_async(dispatch_get_main_queue(), ^{
      [urlData writeToFile:filePath atomically:YES];
    });
  }
});

BOOL fileExists = [[NSFileManager defaultManager] fileExistsAtPath:filePath];
if (fileExists) {
  jsCodeLocation = [[NSURL alloc] initFileURLWithPath:filePath];
} else {
  jsCodeLocation = [[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"];
}
~~~ 

### Some note

This method still have many more enhancement can be done, however its enough to showcase the possibility of react native to asynchronously load file from server, and use the new bundle file when it is ready.
