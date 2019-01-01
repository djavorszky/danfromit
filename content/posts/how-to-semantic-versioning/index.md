---
title: "How to do semantic versioning"
date: 2019-01-01T15:00:00Z
draft: false
featured_image: "posts/how-to-semantic-versioning/images/featured.jpg"
tags: ["semantic version", "semver"]
categories: []
series: ["good to know"]
---

There usually comes a time in our lives when we have to think about versioning our software. Semantic Versioning provides a mostly-standardised way of doing so. How does one use it though?

<!--more-->

What follows is my understanding of the rules outlined on https://semver.org/. If you're more technically inclined, do read about the actual specification on the official site.

Going forward, I'm going to use API and library somewhat interchangeably.

## The idea

![Light bulb](images/lightbulb.jpg)
<sub>Credit to [Free-Photos on pixabay.com](https://pixabay.com/en/light-bulb-lightbulb-light-bulb-1246043/)</sub>

Semantic versions have 3 main parts, separated by periods, with optional pre-release and build metadata tacked to the end. This versioning scheme exists to unify how a change in the software (library/API) is represented. Once we have a good understanding, not only can we rely on libraries and APIs we consume to change in ways we expect them to, but also to provide a more stable experience for consumers of our API or libraries.

https://semver.org/ denotes the three (five) different parts of the semantic version as follows:

MAJOR.MINOR.PATCH, all of them being digits, with two optional sections following PATCH. For example, a library having version 2.3.7 would mean that it's Major version is 2, Minor version is 3 and Patch version is 7.

The optional sections come after PATCH: pre-release and build metadata. We can specify both of them at the same time, though they can appear by themselves as well. A Semantic Version containing all required and optional parts are as follows:

MAJOR.MINOR.PATCH-pre-release+build-metadata

Given the numeric nature of the version numbers, we can also compare versions with one another to decide which one is considered to be "newer" or "better".

## Versions are immutable

There is one point I'd like to emphasise before discussing what each of the sections means:

> Never update an already released version.

It doesn't matter what has changed, whether it's a pre-release or has build-metadata; as soon as the version is out, it is immutable. Any changes done to it has to be done in new versions.

## The meaning

![The meaning](images/meaning.jpg)
<sub>Credit to [stevepb on pixabay.com](https://pixabay.com/en/dictionary-reference-book-learning-1619740/)</sub>

Now that we know the layout of semantic versioning and have the important "before you start" announcement out of the way let's dive into the definitions of each of the sections.

### Patch version: when to update

Patch version increases are all about bug fixes without any side effects. If we discover a bug in our library and fix that, we should only increase the PATCH version, for example, from 2.3.0 to 2.3.1.

That said, security fixes, even if fixing them requires adding new functionalities, should be released as PATCH version updates. The reason here is to encourage the consumers of our library to update to the new version - a patch increase is more likely to be adopted than a minor version increase.

Likewise, if there's an update for a library we rely on that only bumped the PATCH version, we can safely update our dependency, knowing that we're only getting bug fixes.

### Minor version: when to update

Increasing the minor version means adding new functionality that is backwards-compatible. It is important to note that when increasing the minor version, we have to reset the patch version to 0. For example, 2.3.4 becomes 2.4.0.

Same is true for adding internal, non-public facing functionality. Although our "API signature" does not change, we have added new functionality, so the minor version should be increased.

> API signature, in this case, refers to all of the available public-facing endpoints of an API or a library. Adding/modifying/removing private functions do not change the API signature, whereas doing the same with public-facing ones do.

Increasing the minor version doesn't mean that the new version only has new features, however. Fixing bugs can also be part of a minor version increase, as long as there are new features included as well.

### Major version: when to update

The first part of the semantic version called "MAJOR", should be incremented if we introduce a breaking change. Bumping the major version means that we have to reset both the minor and the patch version to 0. For example, 3.7.4 becomes 4.0.0.

> A breaking change is anything that would make the consumers of our API/library need to update their implementation if they want to use the newer version.

Such breaking changes can be anything:

1. Changing the parameter list/return type of a method
2. Removing an existing method/configuration option
3. Switching to another format for config files (e.g. JSON -> yaml) 

Similarly, if we want to use a newer version of a third party library or API, and it has a major version increase (e.g. 2.x.y to 3.x.y), there's a chance that we'll have to update the code consuming the library.

### Pre-release version: when to update

The optional pre-release section comes after the PATCH version, added via a hyphen (-). For example, 2.3.4 is a released version, whereas 2.3.5-alpha isn't. The pre-release version can contain additional periods and hyphens.

This section is used to tag versions that are not yet ready for production use. <https://semver.org> itself had pre-release tags. 2.0.0-rc.1 and 2.0.0-rc.2. These two versions not only tell us that there were two versions before 2.0.0 was finalised, but that they were named release candidate 1 and 2.

The pre-release version does not have to adhere to the requirements of the released version, e.g. we may have breaking changes in a pre-release of a new minor version, as long as the actual released version is backwards-compatible.

### Build metadata: when to update

We can add the build metadata to the end of the semantic version, following either the patch or the pre-release sections. Build metadata should be added with a plus sign (+) to show that it's not a pre-release tag.

The build metadata conveys information about the build itself and is useful when we're doing continuous integration for example. For example, we may build 2.0.0-alpha+20190101 on January first and 2.0.0-alpha+20190102 on the second.

## Version precedence

![The order](images/order.jpg)
<sub>Credit to [Geofreund on pixabay.com](https://pixabay.com/en/geese-flying-flock-of-birds-team-618595/)</sub>

We can order semantic versions if we follow a couple of simple rules; We compare each of the sections from left to right until we find a difference. Build metadata is not taken into account for the precedence, so two versions which only differ in that section are considered to be the same. The above means that:

3.0.0 > 2.5.9 > 2.4.16 > 2.4.13 > 2.4.13-beta.v1 > 2.4.13-beta.v2 > 2.4.13-beta.v3+20180101 == 2.4.13-beta.v3+20180102

## A special case: version 0.x.y

Version 1.0.0 means that our library is released and that it's public API is more or less locked in. We have committed to it, and signal to our consumers that we don't intend to change it frequently.

In some cases, however, especially when starting development, this is not something that we can guarantee. Projects evolve, requirements change, the design may not work out as well as we initially thought.

For this exact reason, we can use Version 0. With that version, we inform the public that the API is subject to change and is somewhat volatile.

The advice <https://semver.org> gives for this is to start versioning from 0.1.0 and for each new feature we add, we should increment the minor version. Once we are confident in what we have built, we should then release it as 1.0.0.

Check out the [Frequently Asked Questions sections on semver.org](https://semver.org/#faq) for more questions-and-answers about when and how to use semantic versions.

Until next time,
Dan

<sub>Featured image credit to [Myriams-Fotos on pixabay.com](https://pixabay.com/en/teacup-cup-of-tea-peppermint-tea-2325722/)</sub>
