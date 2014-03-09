awesome
=======

>awesome is a highly configurable, next generation framework window manager for X. It is primarly targeted at power users, developers and any people dealing with every day computing tasks and who want to have fine-grained control on theirs graphical environment.

##安装##

    root # emerge --ask awesome
    
##启动##

    File~/.xinitrc
    ---
    exec ck-launch-session dbus-launch --sh-syntax --exit-with-session awesome
    
    
##配置##

    user $ mkdir -p ~/.config/awesome/
    user $ cp /etc/xdg/awesome/rc.lua ~/.config/awesome/rc.lua

###设置默认虚拟终端###

    File~/.config/awesome/rc.lua
    ---
    -- This is used later as the default terminal and editor to run.
    terminal = "konsole"
    
###检查配置文件错误###

    user $ awesome -k
    ---
    ✔ Configuration file syntax OK
    
###添加壁纸###

    root # emerge --ask feh
    
>For instance, if you use awsetbg to set your wallpaper, you can write in the theme.lua page that you just selected:
theme.wallpaper_cmd = { "awsetbg -f .config/awesome/themes/awesome-wallpaper.png" }


###Tags###

    Filerc.conf
    -- {{{ Tags
    tags = {}
    for s = 1, screen.count() do
        tags[s] = awful.tag({ "➊", "➋", "➌", "➍" }, s, layouts[1])
    end
    -- }}}
    
###Menu###

    Filerc.conf
    ---
    -- {{{ Menu
    myawesomemenu = {
       { "manual", terminal .. " -e man awesome" },
       { "edit config", editor_cmd .. " " .. awesome.conffile },
       { "reload", awesome.restart },
       { "quit", awesome.quit },
       { "reboot", "reboot" },
       { "shutdown", "shutdown" }
    }
    
    appsmenu = {
       { "urxvt", "urxvt" },
       { "sakura", "sakura" },
       { "ncmpcpp", terminal .. " -e ncmpcpp" },
       { "luakit", "luakit" },
       { "uzbl", "uzbl-browser" },
       { "firefox", "firefox" },
       { "chromium", "chromium" },
       { "thunar", "thunar" },
       { "ranger", terminal .. " -e ranger" },
       { "gvim", "gvim" },
       { "leafpad", "leafpad" },
       { "htop", terminal .. " -e htop" },
       { "sysmonitor", "gnome-system-monitor" }
    }
    
    gamesmenu = {
       { "warsow", "warsow" },
       { "nexuiz", "nexuiz" },
       { "xonotic", "xonotic" },
       { "openarena", "openarena" },
       { "alienarena", "alienarena" },
       { "teeworlds", "teeworlds" },
       { "frozen-bubble", "frozen-bubble" },
       { "warzone2100", "warzone2100" },
       { "wesnoth", "wesnoth" },
       { "supertuxkart", "supertuxkart" },
       { "xmoto" , "xmoto" },
       { "flightgear", "flightgear" },
       { "snes9x" , "snes9x" },
    
    }
    
    mymainmenu = awful.menu({ items = { { "awesome", myawesomemenu },
                                        { "apps", appsmenu },
                        { "games", gamesmenu },
                                        { "terminal", terminal },
                        { "web browser", browser },
                        { "text editor", geditor }
                                      }
                            })
    
    mylauncher = awful.widget.launcher({ image = image(beautiful.awesome_icon),
                                         menu = mymainmenu })
    -- }}}























    
