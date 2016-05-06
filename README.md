-   [Contents](index.html)
-   [Index](doc-index.html)

xmonad-prime-monad-0.1.0.0: True monadic config for XMonad

|              |                                          |
|:-------------|:-----------------------------------------|
| Copyright    | Nikolay Yakimov &lt;root@livid.pp.ru&gt; |
| License      | BSD-style (see LICENSE)                  |
| Maintainer   | Nikolay Yakimov &lt;root@livid.pp.ru&gt; |
| Stability    | unstable                                 |
| Portability  | unportable                               |
| Safe Haskell | None                                     |
| Language     | Haskell2010                              |

XMonad.Config.Prime.Monadic

Contents

-   [Start here](#g:1)
-   [Attributes you can set](#g:2)
-   [Attributes you can add to](#g:3)
-   [Attributes you can add to or remove from](#g:4)
-   [Modifying the list of workspaces](#g:5)
-   [Modifying the screen keybindings](#g:6)
-   [Modifying the layoutHook](#g:7)
-   [Updating the XConfig en masse](#g:8)
-   [The rest of the world](#g:9)
-   [Core](#g:10)
-   [Example config](#g:11)
-   [Troubleshooting](#g:12)

Description

This is a draft of a brand new config syntax for xmonad. It aims to be:

-   easier to copy/paste snippets from the docs
-   easier to get the gist for what's going on, for you imperative programmers

It's brand new, so it's pretty much guaranteed to break or change syntax. But what's the worst that could happen? Xmonad crashes and logs you out? It probably won't do that. Give it a try.

Synopsis

-   [xmonad](#v:xmonad) :: [Prime](XMonad-Config-Prime-Monadic.html#t:Prime) -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ()
-   [nothing](#v:nothing) :: [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [normalBorderColor](#v:normalBorderColor) :: Settable [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [focusedBorderColor](#v:focusedBorderColor) :: Settable [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [terminal](#v:terminal) :: Settable [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [modMask](#v:modMask) :: Settable [KeyMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:KeyMask) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [borderWidth](#v:borderWidth) :: Settable [Dimension](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Xlib-Types.html#t:Dimension) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [focusFollowsMouse](#v:focusFollowsMouse) :: Settable [Bool](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Bool.html#t:Bool) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [clickJustFocuses](#v:clickJustFocuses) :: Settable [Bool](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Bool.html#t:Bool) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   <span class="keyword">class</span> [SettableClass](#t:SettableClass) s x y | s -&gt; x y <span class="keyword">where</span>
    -   [(=:)](#v:-61-:) :: s c -&gt; y -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) c
-   <span class="keyword">class</span> [UpdateableClass](#t:UpdateableClass) s x y | s -&gt; x y <span class="keyword">where</span>
    -   [(=.)](#v:-61-.) :: s c -&gt; (x -&gt; y) -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) c
-   [manageHook](#v:manageHook) :: Summable [ManageHook](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:ManageHook) [ManageHook](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:ManageHook) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [handleEventHook](#v:handleEventHook) :: Summable ([Event](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Xlib-Extras.html#t:Event) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) [All](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Monoid.html#t:All)) ([Event](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Xlib-Extras.html#t:Event) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) [All](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Monoid.html#t:All)) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [workspaces](#v:workspaces) :: Summable \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [logHook](#v:logHook) :: Summable ([X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ()) ([X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ()) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [startupHook](#v:startupHook) :: Summable ([X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ()) ([X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ()) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [clientMask](#v:clientMask) :: Summable [EventMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:EventMask) [EventMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:EventMask) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [rootMask](#v:rootMask) :: Summable [EventMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:EventMask) [EventMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:EventMask) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   <span class="keyword">class</span> [SummableClass](#t:SummableClass) s y | s -&gt; y <span class="keyword">where</span>
    -   [(=+)](#v:-61--43-) :: s c -&gt; y -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) c
-   [keys](#v:keys) :: Keys ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   [mouseBindings](#v:mouseBindings) :: MouseBindings ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)
-   <span class="keyword">class</span> [RemovableClass](#t:RemovableClass) r y | r -&gt; y <span class="keyword">where</span>
    -   [(=-)](#v:-61--45-) :: r c -&gt; y -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) c
-   [withWorkspaces](#v:withWorkspaces) :: [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) WorkspaceConfig -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [wsNames](#v:wsNames) :: Settable \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] WorkspaceConfig
-   [wsKeys](#v:wsKeys) :: Summable \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] WorkspaceConfig
-   [wsActions](#v:wsActions) :: Summable \[([String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String), [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ())\] \[([String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String), [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ())\] WorkspaceConfig
-   [wsSetName](#v:wsSetName) :: [Int](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Int.html#t:Int) -&gt; [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) WorkspaceConfig
-   [withScreens](#v:withScreens) :: IsLayout l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) ScreenConfig -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [sKeys](#v:sKeys) :: Summable \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] ScreenConfig
-   [sActions](#v:sActions) :: Summable \[([String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String), [ScreenId](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:ScreenId) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ())\] \[([String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String), [ScreenId](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:ScreenId) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ())\] ScreenConfig
-   [onScreens](#v:onScreens) :: [Eq](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Eq.html#t:Eq) s =&gt; (i -&gt; [StackSet](file:///usr/share/doc/xmonad-0.12/html/XMonad-StackSet.html#t:StackSet) i l a s sd -&gt; [StackSet](file:///usr/share/doc/xmonad-0.12/html/XMonad-StackSet.html#t:StackSet) i l a s sd) -&gt; s -&gt; [StackSet](file:///usr/share/doc/xmonad-0.12/html/XMonad-StackSet.html#t:StackSet) i l a s sd -&gt; [StackSet](file:///usr/share/doc/xmonad-0.12/html/XMonad-StackSet.html#t:StackSet) i l a s sd
-   [addLayout](#v:addLayout) :: IsLayout r [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; r [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [resetLayout](#v:resetLayout) :: IsLayout r [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; r [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [modifyLayout](#v:modifyLayout) :: [CC](XMonad-Config-Prime-Monadic.html#t:CC) m [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; (<span class="keyword">forall</span> l. [LayoutClass](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:LayoutClass) l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) -&gt; m l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window)) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [squash](#v:squash) :: S f t =&gt; (l a -&gt; f a) -&gt; l a -&gt; t a
-   [startWith](#v:startWith) :: IsLayout l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [apply](#v:apply) :: ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout) -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout)) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [apply'](#v:apply-39-) :: [CC](XMonad-Config-Prime-Monadic.html#t:CC) m [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; (<span class="keyword">forall</span> l. [LayoutClass](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:LayoutClass) l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) (m l)) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [squashXC](#v:squashXC) :: S f t =&gt; ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) f) -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) t
-   [applyIO](#v:applyIO) :: ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout) -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout))) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [applyIO'](#v:applyIO-39-) :: [CC](XMonad-Config-Prime-Monadic.html#t:CC) m [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; (<span class="keyword">forall</span> l. [LayoutClass](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:LayoutClass) l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) (m l))) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)
-   [squashIO](#v:squashIO) :: S f t =&gt; ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) f)) -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) t)
-   module [XMonad](file:///usr/share/doc/xmonad-0.12/html/XMonad.html)
-   <span class="keyword">type</span> [Prime](#t:Prime) = [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout))
-   <span class="keyword">type</span> [Arr](#t:Arr) a = [StateT](file:///usr/share/doc/mtl-2.2.1-r1/html/Control-Monad-State-Lazy.html#t:StateT) a [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ()
-   <span class="keyword">class</span> [CC](#t:CC) m a <span class="keyword">where</span>
    -   [dict](#v:dict) :: <span class="keyword">forall</span> l. IsLayout l a =&gt; m l a -&gt; [Dict](XMonad-Config-Prime-Monadic.html#t:Dict) (IsLayout (m l) a)
-   <span class="keyword">data</span> [Dict](#t:Dict) :: [Constraint](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/GHC-Exts.html#t:Constraint) -&gt; \* <span class="keyword">where</span>
    -   [Dict](#v:Dict) :: a =&gt; [Dict](XMonad-Config-Prime-Monadic.html#t:Dict) a

Start here
==========

To start with, create a `~/.xmonad/xmonad.hs` that looks like this:

    import XMonad.Config.Prime.Monadic

    -- Imports go here.

    main = xmonad $ do
      nothing
      -- Configs go here.

This will give you a default xmonad install, with room to grow. The lines starting with double dashes are comments. You may delete them. Note that Haskell is a bit precise about indentation. Make sure all the statements in your do-block start at the same column, and make sure that any multi-line statements are formatted with a hanging indent. (For an example, see the 'keys =+' statement in the *Example config* section, below.)

After changing your config file, restart xmonad with mod-q (where, by default, "mod" == "alt").

<a href="" class="def">xmonad</a> :: [Prime](XMonad-Config-Prime-Monadic.html#t:Prime) -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ()

This is the xmonad main function. It passes `def` (the default `XConfig`) into your do-block, takes the modified config out The do-block is a 'Prime. Advanced readers can skip right to that definition.

<a href="" class="def">nothing</a> :: [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

This doesn't modify the config in any way. It's just here for your initial config because Haskell doesn't allow empty do-blocks. Feel free to delete it

Attributes you can set
======================

These are a bunch of attributes that you can set. Syntax looks like this:

      terminal =: "urxvt"

Strings are double quoted, Dimensions are unquoted integers, booleans are `True` or `False` (case-sensitive), and `modMask` is usually `mod1Mask` or `mod4Mask`.

<a href="" class="def">normalBorderColor</a> :: Settable [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

Non-focused windows border color. Default: `"#dddddd"`

<a href="" class="def">focusedBorderColor</a> :: Settable [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

Focused windows border color. Default: `"#ff0000"`

<a href="" class="def">terminal</a> :: Settable [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

The preferred terminal application. Default: `"xterm"`

<a href="" class="def">modMask</a> :: Settable [KeyMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:KeyMask) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

The mod modifier, as used by key bindings. Default: `mod1Mask` (which is probably alt on your computer).

<a href="" class="def">borderWidth</a> :: Settable [Dimension](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Xlib-Types.html#t:Dimension) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

The border width (in pixels). Default: `1`

<a href="" class="def">focusFollowsMouse</a> :: Settable [Bool](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Bool.html#t:Bool) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

Whether window focus follows the mouse cursor on move, or requires a mouse click. (Mouse? What's that?) Default: `True`

<a href="" class="def">clickJustFocuses</a> :: Settable [Bool](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Bool.html#t:Bool) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

If True, a mouse click on an inactive window focuses it, but the click is not passed to the window. If False, the click is also passed to the window. Default `True`

<span class="keyword">class</span> <a href="" class="def">SettableClass</a> s x y | s -&gt; x y <span class="keyword">where</span>

Methods

<a href="" class="def">(=:)</a> :: s c -&gt; y -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) c

This lets you modify an attribute.

Instances

|                                                                                                                                                                                          |  |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-|
| <span class="inst-left">[UpdateableClass](XMonad-Config-Prime-Monadic.html#t:UpdateableClass) s x y =&gt; [SettableClass](XMonad-Config-Prime-Monadic.html#t:SettableClass) s x y</span> |  |

<span class="keyword">class</span> <a href="" class="def">UpdateableClass</a> s x y | s -&gt; x y <span class="keyword">where</span>

Methods

<a href="" class="def">(=.)</a> :: s c -&gt; (x -&gt; y) -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) c

This lets you apply a function to an attribute (i.e. read, modify, write).

Attributes you can add to
=========================

In addition to being able to set these attributes, they have a special syntax for being able to add to them. The operator is `=+` (the plus comes *after* the equals), but each attribute has a different syntax for what comes after the operator.

<a href="" class="def">manageHook</a> :: Summable [ManageHook](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:ManageHook) [ManageHook](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:ManageHook) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

The action to run when a new window is opened. Default:

      manageHook =: composeAll [className =? "MPlayer" --> doFloat, className =? "Gimp" --> doFloat]

To add more rules to this list, you can say, for instance:

    import XMonad.StackSet
    ...
      manageHook =+ (className =? "Emacs" --> doF kill)
      manageHook =+ (className =? "Vim" --> doF shiftMaster)

Note that operator precedence mandates the parentheses here.

<a href="" class="def">handleEventHook</a> :: Summable ([Event](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Xlib-Extras.html#t:Event) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) [All](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Monoid.html#t:All)) ([Event](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Xlib-Extras.html#t:Event) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) [All](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Monoid.html#t:All)) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

Custom X event handler. Return `All True` if the default handler should also be run afterwards. Default does nothing. To add an event handler:

    import XMonad.Hooks.ServerMode
    ...
      handleEventHook =+ serverModeEventHook

<a href="" class="def">workspaces</a> :: Summable \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

List of workspaces' names. Default: `map show [1 .. 9 :: Int]`. Adding appends to the end:

      workspaces =+ ["0"]

This is useless unless you also create keybindings for this.

<a href="" class="def">logHook</a> :: Summable ([X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ()) ([X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ()) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

The action to perform when the windows set is changed. This happens whenever focus change, a window is moved, etc. `logHook =+` takes an `X ()` and appends it via '(&gt;&gt;)'. For instance:

    import XMonad.Hooks.ICCCMFocus
    ...
      logHook =+ takeTopFocus

Note that if your expression is parametrically typed (e.g. of type `MonadIO m => m ()`), you'll need to explicitly annotate it, like so:

      logHook =+ (io $ putStrLn "Hello, world!" :: X ())

<a href="" class="def">startupHook</a> :: Summable ([X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ()) ([X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ()) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

The action to perform on startup. `startupHook =+` takes an `X ()` and appends it via '(&gt;&gt;)'. For instance:

    import XMonad.Hooks.SetWMName
    ...
      startupHook =+ setWMName "LG3D"

Note that if your expression is parametrically typed (e.g. of type `MonadIO m => m ()`), you'll need to explicitly annotate it, as documented in `logHook`.

<a href="" class="def">clientMask</a> :: Summable [EventMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:EventMask) [EventMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:EventMask) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

The client events that xmonad is interested in. This is useful in combination with handleEventHook. Default: `structureNotifyMask .|.  enterWindowMask .|. propertyChangeMask`

      clientMask =+ keyPressMask .|. keyReleaseMask

<a href="" class="def">rootMask</a> :: Summable [EventMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:EventMask) [EventMask](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:EventMask) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

The root events that xmonad is interested in. This is useful in combination with handleEventHook. Default: `substructureRedirectMask .|.  substructureNotifyMask .|. enterWindowMask .|. leaveWindowMask .|.  structureNotifyMask .|. buttonPressMask`

<span class="keyword">class</span> <a href="" class="def">SummableClass</a> s y | s -&gt; y <span class="keyword">where</span>

Methods

<a href="" class="def">(=+)</a> :: s c -&gt; y -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) c <span class="fixity">infix 0</span><span class="rightedge"></span>

This lets you add to an attribute.

Attributes you can add to or remove from
========================================

The following support the the `=+` for adding items and the `=-` operator for removing items.

<a href="" class="def">keys</a> :: Keys ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

Key bindings to `X` actions. Default: see `` `man xmonad` ``. `keys` takes a list of keybindings specified emacs-style, as documented in `mkKeyMap`. For example, to change the "kill window" key:

      keys =- ["M-S-c"]
      keys =+ [("M-M1-x", kill)]

<a href="" class="def">mouseBindings</a> :: MouseBindings ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l)

Mouse button bindings to an `X` actions on a window. Default: see `` `man  xmonad` ``. To make mod-[scrollwheel](scrollwheel) switch workspaces:

    import XMonad.Actions.CycleWS (nextWS, prevWS)
    ...
      mouseBindings =+ [((mod4Mask, button4), const prevWS),
                        ((mod4Mask, button5), const nextWS)]

Note that you need to specify the numbered mod-mask e.g. `mod4Mask` instead of just `modMask`.

<span class="keyword">class</span> <a href="" class="def">RemovableClass</a> r y | r -&gt; y <span class="keyword">where</span>

Methods

<a href="" class="def">(=-)</a> :: r c -&gt; y -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) c <span class="fixity">infix 0</span><span class="rightedge"></span>

This lets you remove from an attribute.

Modifying the list of workspaces
================================

Workspaces can be configured through `workspaces`, but then the `keys` need to be set, and this can be a bit laborious. `withWorkspaces` provides a convenient mechanism for common workspace updates.

<a href="" class="def">withWorkspaces</a> :: [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) WorkspaceConfig -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Configure workspaces through a Prime-like interface. Example:

      withWorkspaces $ do
        wsKeys =+ ["0"]
        wsActions =+ [("M-M1-", windows . swapWithCurrent)]
        wsSetName 1 "mail"

This will set `workspaces` and add the necessary keybindings to `keys`. Note that it won't remove old keybindings; it's just not that clever.

<a href="" class="def">wsNames</a> :: Settable \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] WorkspaceConfig

The list of workspace names, like `workspaces` but with two differences:

1.  If any entry is the empty string, it'll be replaced with the corresponding entry in `wsKeys`.
2.  The list is truncated to the size of `wsKeys`.

The default value is `repeat` "".

If you'd like to create workspaces without associated keyspecs, you can do that afterwards, outside the `withWorkspaces` block, with `workspaces` =+.

<a href="" class="def">wsKeys</a> :: Summable \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] WorkspaceConfig

The list of workspace keys. These are combined with the modifiers in `wsActions` to form the keybindings for navigating to workspaces. Default: `["1","2",...,"9"]`.

<a href="" class="def">wsActions</a> :: Summable \[([String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String), [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ())\] \[([String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String), [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ())\] WorkspaceConfig

Mapping from key prefix to command. Its type is `[(String, String ->  X())]`. The key prefix may be a modifier such as `"M-"`, or a submap prefix such as `"M-a "`, or both, as in `"M-a M-"`. The command is a function that takes a workspace name and returns an `X ()`. `withWorkspaces` creates keybindings for the cartesian product of `wsKeys` and `wsActions`.

Default:

    [("M-", windows . W.greedyView),
     ("M-S-", windows . W.shift)]

<a href="" class="def">wsSetName</a> :: [Int](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Int.html#t:Int) -&gt; [String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String) -&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) WorkspaceConfig

A convenience for just modifying one entry in `wsNames`, in case you only want a few named workspaces. Example:

        wsSetName 1 "mail"
        wsSetName 2 "web"

Modifying the screen keybindings
================================

`withScreens` provides a convenient mechanism to set keybindings for moving between screens, much like `withWorkspaces`.

<a href="" class="def">withScreens</a> :: IsLayout l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) ScreenConfig -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Configure screen keys through a Prime-like interface:

      withScreens $ do
        sKeys =: ["e", "r"]

This will add the necessary keybindings to `keys`. Note that it won't remove old keybindings; it's just not that clever.

<a href="" class="def">sKeys</a> :: Summable \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] \[[String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String)\] ScreenConfig

The list of screen keys. These are combined with the modifiers in `sActions` to form the keybindings for navigating to workspaces. Default: `["w","e","r"]`.

<a href="" class="def">sActions</a> :: Summable \[([String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String), [ScreenId](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:ScreenId) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ())\] \[([String](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-String.html#t:String), [ScreenId](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:ScreenId) -&gt; [X](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:X) ())\] ScreenConfig

Mapping from key prefix to command. Its type is `[(String, ScreenId ->  X())]`. Works the same as `wsActions` except for a different function type.

Default:

    [("M-", windows . onScreens W.view),
     ("M-S-", windows . onScreens W.shift)]

<a href="" class="def">onScreens</a> :: [Eq](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Eq.html#t:Eq) s =&gt; (i -&gt; [StackSet](file:///usr/share/doc/xmonad-0.12/html/XMonad-StackSet.html#t:StackSet) i l a s sd -&gt; [StackSet](file:///usr/share/doc/xmonad-0.12/html/XMonad-StackSet.html#t:StackSet) i l a s sd) -&gt; s -&gt; [StackSet](file:///usr/share/doc/xmonad-0.12/html/XMonad-StackSet.html#t:StackSet) i l a s sd -&gt; [StackSet](file:///usr/share/doc/xmonad-0.12/html/XMonad-StackSet.html#t:StackSet) i l a s sd

Converts a stackset transformer parameterized on the workspace type into one parameterized on the screen type. For example, you can use `onScreens W.view  0` to navigate to the workspace on the 0th screen. If the screen id is not recognized, the returned transformer acts as an identity function.

Modifying the layoutHook
========================

Layouts are special. You can't modify them using the `=:` or `=.` operator. You need to use the following functions.

<a href="" class="def">addLayout</a> :: IsLayout r [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; r [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Add a layout to the list of layouts choosable with mod-space. For instance:

    import XMonad.Layout.Tabbed
    ...
      addLayout simpleTabbed

<a href="" class="def">resetLayout</a> :: IsLayout r [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; r [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Reset the layoutHook from scratch. For instance, to get rid of the wide layout:

      resetLayout $ Tall 1 (3/100) (1/2) ||| Full

(The dollar is like an auto-closing parenthesis, so all the stuff to the right of it is treated like an argument to resetLayout.)

<a href="" class="def">modifyLayout</a> :: [CC](XMonad-Config-Prime-Monadic.html#t:CC) m [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; (<span class="keyword">forall</span> l. [LayoutClass](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:LayoutClass) l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) -&gt; m l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window)) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Modify your `layoutHook` with some wrapper function. You probably want to call this after you're done calling `addLayout`.

Note that because of existential type in the `Prime` monad, `modifyLayout` can only accept modifiers that are instances of `CC`. This also entails that something like this will not work:

    modifyLayout $ smartBorders . avoidStruts

You can use `squash` to make it work though:

    modifyLayout $ squash $ smartBorders . avoidStruts

TL;DR -- apply modifiers separately, if you can.

Example:

    import XMonad.Layout.NoBorders
    ...
      modifyLayout smartBorders

<a href="" class="def">squash</a> :: S f t =&gt; (l a -&gt; f a) -&gt; l a -&gt; t a

Squashes a type m1 (m2 l) a into m3 l a. Use with `modifyLayout` if you need to apply it to function that adds more than one modifier to layout

Example:

    let myLayoutFunction = Mirror . Mirror . Mirror . Mirror

    modifyLayout $ squash $ myLayoutFunction

Updating the XConfig en masse
=============================

Finally, there are a few contrib modules that bundle multiple attribute updates together. There are three types: 1) wholesale replacements for the default config, 2) pure functions on the config, and 3) IO actions on the config. Each of those can also modify layout. The syntax for each is different. Examples:

1) To start with a `gnomeConfig` instead of the default, we use `startWith`:

    import XMonad.Config.Gnome
    ...
      startWith gnomeConfig

2) `withUrgencyHook` is a pure function, so we need to use `apply`:

    import XMonad.Hooks.UrgencyHook
    ...
      apply $ withUrgencyHook dzenUrgencyHook

3) `fullscreenSupport` is a pure function, but it also applies a modifier to layout. In this case we need to use `apply'`:

    import XMonad.Layout.Fullscreen
    ...
      apply' fullscreenSupport

4) `xmobar` returns an `IO (XConfig (ModifiedLayout AvoidStruts l))`, so we need to use `applyIO'`:

    import XMonad.Hooks.DynamicLog
    ...
      applyIO' xmobar

<a href="" class="def">startWith</a> :: IsLayout l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Replace the current `XConfig` with the given one. If you use this, you probably want it to be the first line of your config.

<a href="" class="def">apply</a> :: ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout) -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout)) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Turns a pure function on `XConfig` into a 'Prime.

<a href="" class="def">apply'</a> :: [CC](XMonad-Config-Prime-Monadic.html#t:CC) m [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; (<span class="keyword">forall</span> l. [LayoutClass](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:LayoutClass) l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) (m l)) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Turns a pure function on `XConfig` into a 'Prime. This version also accepts functions that change layout. Use `squashXC` for functions adding more than one layout modifier:

    apply' $ squashXC myFunction

<a href="" class="def">squashXC</a> :: S f t =&gt; ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) f) -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) t

Same as `squash`, but acts on XConfig. Use with `apply'`.

Example:

    let myLayoutFunction x = mirror $ mirror $ mirror $ mirror $ x
        mirror xc = xc{X.layoutHook = Mirror $ X.layoutHook xc}

    apply $ squashXC $ myLayoutFunction

<a href="" class="def">applyIO</a> :: ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout) -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout))) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Turns an IO function on `XConfig` into a 'Prime.

<a href="" class="def">applyIO'</a> :: [CC](XMonad-Config-Prime-Monadic.html#t:CC) m [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; (<span class="keyword">forall</span> l. [LayoutClass](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:LayoutClass) l [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window) =&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) (m l))) -&gt; [Prime](XMonad-Config-Prime-Monadic.html#t:Prime)

Turns an IO function on `XConfig` into a 'Prime. This version also accepts functions that change layout. Use `squashIO` for functions adding more than one layout modifier:

    applyIO' $ squashIO myFunction

<a href="" class="def">squashIO</a> :: S f t =&gt; ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) f)) -&gt; [XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) l -&gt; [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) t)

Same as `squashXC`, but for `IO` functions. Use with `applyIO'`

Example:

    let myLayoutFunction x = return $ mirror $ mirror $ mirror $ mirror $ x
        mirror xc = xc{X.layoutHook = Mirror $ X.layoutHook xc}

    applyIO $ squashIO $ myLayoutFunction

The rest of the world
=====================

Everything you know and love from the core [XMonad](file:///usr/share/doc/xmonad-0.12/html/XMonad.html) module is available for use in your config file, too.

module [XMonad](file:///usr/share/doc/xmonad-0.12/html/XMonad.html)

Core
====

These are the building blocks on which the config language is built. Regular people shouldn't need to know about these.

<span class="keyword">type</span> <a href="" class="def">Prime</a> = [Arr](XMonad-Config-Prime-Monadic.html#t:Arr) ([XConfig](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:XConfig) [Layout](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Layout))

A Prime is a state monad that incapsulates an XConfig. It wraps layouts into an existential type.

<span class="keyword">type</span> <a href="" class="def">Arr</a> a = [StateT](file:///usr/share/doc/mtl-2.2.1-r1/html/Control-Monad-State-Lazy.html#t:StateT) a [IO](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/System-IO.html#t:IO) ()

An Arr is a generalization of Prime. Don't reference the type, if you can avoid it. It might go away in the future.

<span class="keyword">class</span> <a href="" class="def">CC</a> m a <span class="keyword">where</span>

Typeclass used to prove that there is actually a layout inside `Layout`.

All layout modifiers like `Mirror` must be instances of this class. Most instances should be already defined. If not, in most cases you can define one with

    instance CC Mod a where dict _ = Dict

Where Mod is your modifier.

All modifiers that are instances of `LayoutModifier` are automatically instances of `CC`.

Methods

<a href="" class="def">dict</a> :: <span class="keyword">forall</span> l. IsLayout l a =&gt; m l a -&gt; [Dict](XMonad-Config-Prime-Monadic.html#t:Dict) (IsLayout (m l) a)

Instances

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |  |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-|
| <span class="inst-left">[CC](XMonad-Config-Prime-Monadic.html#t:CC) [Mirror](file:///usr/share/doc/xmonad-0.12/html/XMonad-Layout.html#t:Mirror) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |  |
| <span class="inst-left">[CC](XMonad-Config-Prime-Monadic.html#t:CC) [WithID](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-Groups.html#t:WithID) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |  |
| <span class="inst-left">IsLayout l a =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([Choose](file:///usr/share/doc/xmonad-0.12/html/XMonad-Layout.html#t:Choose) l) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |  |
| <span class="inst-left">IsLayout l a =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([NewSelect](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-LayoutCombinators.html#t:NewSelect) l) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |  |
| <span class="inst-left">(IsLayout l a, [Show](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Show.html#t:Show) a) =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([OnHost](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-OnHost.html#t:OnHost) l) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |  |
| <span class="inst-left">[Message](file:///usr/share/doc/xmonad-0.12/html/XMonad-Core.html#t:Message) m =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([Ignore](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-MessageControl.html#t:Ignore) m) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |  |
| <span class="inst-left">[LayoutModifier](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-LayoutModifier.html#t:LayoutModifier) m a =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([ModifiedLayout](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-LayoutModifier.html#t:ModifiedLayout) m) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |  |
| <span class="inst-left">IsLayout l a =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([ToggleLayouts](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-ToggleLayouts.html#t:ToggleLayouts) l) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |  |
| <span class="inst-left">IsLayout l a =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([IfMax](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-IfMax.html#t:IfMax) l) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |  |
| <span class="inst-left">([Eq](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Eq.html#t:Eq) a, [Read](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Read.html#t:Read) a, [Show](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Show.html#t:Show) a, [Typeable](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Typeable-Internal.html#t:Typeable) \* a, IsLayout l a) =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([LayoutN](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-LayoutBuilder.html#t:LayoutN) l) a</span>                                                                                                                                                                                                                                                                                                               |  |
| <span class="inst-left">([Read](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Read.html#t:Read) b, [Show](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Show.html#t:Show) b, [Typeable](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Typeable-Internal.html#t:Typeable) \* a, [HList](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-MultiToggle.html#t:HList) b a) =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([MultiToggle](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-MultiToggle.html#t:MultiToggle) b) a</span>                                                                                                                                                                                                                                                                                                           |  |
| <span class="inst-left">(IsLayout l a, [Show](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Show.html#t:Show) a) =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([PerScreen](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-PerScreen.html#t:PerScreen) l) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |  |
| <span class="inst-left">(IsLayout l a, [Show](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Show.html#t:Show) a) =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([PerWorkspace](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-PerWorkspace.html#t:PerWorkspace) l) a</span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |  |
| <span class="inst-left">(IsLayout l (), IsLayout l1 [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window), IsLayout l2 [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window)) =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([CombineTwoP](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-ComboP.html#t:CombineTwoP) (l ()) l1) [Window](file:///usr/share/doc/x11-1.6.1.2/html/Graphics-X11-Types.html#t:Window)</span>                                                                                                                                                                                                                                                                                                                                                                                                                                 |  |
| <span class="inst-left">(IsLayout l (), IsLayout l1 a, [Read](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Read.html#t:Read) a, [Show](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Show.html#t:Show) a, [Eq](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Eq.html#t:Eq) a, [Typeable](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Typeable-Internal.html#t:Typeable) \* a) =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([CombineTwo](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-Combo.html#t:CombineTwo) (l ()) l1) a</span>                                                                                                                                                                                                                                                                                         |  |
| <span class="inst-left">(IsLayout l a, [Show](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Show.html#t:Show) a, [Eq](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Eq.html#t:Eq) a, [Read](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Read.html#t:Read) b, [Read](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Read.html#t:Read) a, [Show](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Text-Show.html#t:Show) b, [Typeable](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/Data-Typeable-Internal.html#t:Typeable) \* a, [Predicate](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-LayoutBuilderP.html#t:Predicate) b a) =&gt; [CC](XMonad-Config-Prime-Monadic.html#t:CC) ([LayoutP](file:///usr/share/doc/xmonad-contrib-0.12/html/XMonad-Layout-LayoutBuilderP.html#t:LayoutP) b l) a</span> |  |

<span class="keyword">data</span> <a href="" class="def">Dict</a> :: [Constraint](file:///usr/share/doc/ghc-7.10.3/html/libraries/base-4.8.2.0/GHC-Exts.html#t:Constraint) -&gt; \* <span class="keyword">where</span>

Constructors

|                                                                                              |  |
|:---------------------------------------------------------------------------------------------|:-|
| <a href="" class="def">Dict</a> :: a =&gt; [Dict](XMonad-Config-Prime-Monadic.html#t:Dict) a |  |

Example config
==============

As an example, I've included below a subset of my current config. Note that my import statements specify individual identifiers in parentheticals. That's optional. The default is to import the entire module. I just find it helpful to remind me where things came from.

    import XMonad.Config.Prime

    import XMonad.Actions.CycleWS (prevWS, nextWS)
    import XMonad.Actions.SwapWorkspaces (swapWithCurrent)
    import XMonad.Actions.WindowNavigation (withWindowNavigation)
    import XMonad.Layout.Fullscreen (fullscreenSupport)
    import XMonad.Layout.NoBorders (smartBorders)
    import XMonad.Layout.Tabbed (simpleTabbed)

    main = xmonad $ do
      modMask =: mod4Mask
      normalBorderColor =: "#222222"
      terminal =: "urxvt"
      focusFollowsMouse =: False
      resetLayout $ Tall 1 (3/100) (1/2) ||| simpleTabbed
      modifyLayout smartBorders
      apply fullscreenSupport
      applyIO' $ withWindowNavigation (xK_w, xK_a, xK_s, xK_d)
      withWorkspaces $ do
        wsKeys =+ ["0"]
        wsActions =+ [("M-M1-", windows . swapWithCurrent)]
      keys =+ [
          ("M-,",                      sendMessage $ IncMasterN (-1)),
          ("M-.",                      sendMessage $ IncMasterN 1),
          ("M-M1-d",                   spawn "date | dzen2 -fg '#eeeeee' -p 2"),
          ("C-S-q",                    return ()),
          ("<XF86AudioLowerVolume>",   spawn "amixer set Master 5%-"),
          ("<XF86AudioRaiseVolume>",   spawn "amixer set Master 5%+"),
          ("M-M1-x",                   kill),
          ("M-i",                      prevWS),
          ("M-o",                      nextWS)
        ]

Troubleshooting
===============

### How do I use the old keyboard syntax?

You can use `apply` and supply your own Haskell function. For instance:

    apply $ flip additionalKeys $ [((mod1Mask, xK_z), spawn "date | dzen2 -fg '#eeeeee' -p 2")]

### How do I run a command before xmonad starts (like `spawnPipe`)?

If you're using it for a status bar, see if `dzen` or `xmobar` does what you want. If so, you can apply it with `applyIO`.

If not, you can write your own `XConfig l -> IO (XConfig l)` and apply it with `applyIO`.

Alternatively, you could do something like this this:

    import qualified Prelude as P (>>)

    main =
      openFile ".xmonad.log" AppendMode >>= \log ->
      hSetBuffering log LineBuffering P.>>
      (xmonad $ do
         nothing -- Prime config here.
      )

Produced by [Haddock](http://www.haskell.org/haddock/) version 2.16.1
