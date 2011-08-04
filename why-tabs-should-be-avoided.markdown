---
layout: page
supertitle: "2011 Hacker's Coding Style Guide"
superlink: "./"
title: "Why tabs should be avoided?"
comments: true
sharing: true
footer: true
---

Tabs might seem like a good idea initially, so it's important to elaborate why exactly they should be avoided.

Consider the following code:

    namespace something
    {
        SomeClass::SomeClass()
            : InheritingClass(false, false
                              5, 10, true,
                              bleh, blah)
        {
            if (true)    //This should be replaced
            {            //with a proper boolean
                func();
            }
        };
    }

The only way to lay it out with tabs is like this (`____` is a tab, `.` is a space):

    namespace something
    {
    ____SomeClass::SomeClass()
    ________:.InheritingClass(false, false
    ________..................5, 10, true,
    ________..................bleh, blah)
    ____{
    ________if.(true)....//This should be replaced
    ________{............//with a proper boolean
    ________....func();
    ________}
    ____};
    }

This actually requires mixing tabs and spaces. If you simply used tabs for all indentation, any tab size setting different from 4 would result in misaligned code.

So the downsides of tabs are:

1. Hard to align code beyond simple indenting, like in the example above. Your editor won't do it automatically.
2. When using tabs, spaces are still valid characters. Did you just accidentally indent with spaces instead of tabs? You never know. You have to enable a noisy visual whitespace to see it.
3. Someone, somewhere will display your code expanding tabs to 8 spaces. Try diff or cat on the command line.
4. If you ban tabs, it is easy to write a pre-commit hook (or an editor macro, or a command-line tool) to check that no tabs are being added. It's much harder (or even impossible) to verify that the indentation is correct when using tabs.
5. If you can always get #1 and #2 right, one of your collegues or contributors won't.

Someone might propose to store tabs in the version control system and use hooks (like git attributes) to convert to the favorite indentation style on checkout, and convert back on commit. This is a bad idea because:

1. Observe that it is impossible to automatically convert spaces into tabs if you have at least a single case of complex code alignment.
2. Doing such post-checkout/pre-commit conversions is a bad idea in general because it does not work outside your version control system. Some day you will want to copy-paste a piece of code to a colleague, or to use an external diff/patch/merge tool.
