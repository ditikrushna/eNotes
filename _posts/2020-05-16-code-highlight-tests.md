---
layout: post
title: "CPC Test NITT (Tempo. Post)"
categories: misc
---

## Cake_Event___ 
    #include<bits/stdc++.h>
    using namespace std;
    typedef long long int lli;
    int main()
    {
         lli n,k,t;
         cin>>n>>k;
         vector<lli> a;lli sum=0;
         a.push_back(0);
         for(int i=1;i<=n;i++)
         {
             cin>>t;
             sum+=t;
             a.push_back(sum);
         }
         lli max=a[k]-a[0];
         for(lli i=0;i<=n-k;i++)
         {
             if(a[i+k]-a[i]>max)
             {
                 max=a[k+i]-a[i];
             }
         }
         cout<<max;
         return 0;
    } 



## Heads and Tails 

```#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;


int main() {
  
    int n;
    cin >> n ;
    
    vector<string> a(n);
    vector<int> dp(n);
    
    int heads = 0;
    
    for(int i = 0; i < n; ++i) {
        cin >> a[i];
        
        if(a[i] == "H") heads++;
    }
    
    if(a[0] == "H") {
        dp[0] = -1;
    } else {
        dp[0] = 1;
    }
    
    for(int i = 1; i < n; ++i) {
        if(a[i] == "H") {
            dp[i] = max(dp[i-1] - 1, -1);
        } else {
            dp[i] = max(dp[i-1] + 1, 1);
        }
    }
    
    cout << *max_element(dp.begin(), dp.end()) + heads << endl;
    
    return 0;
}
```

## Test for Perl

```#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
#include <queue>
using namespace std;

struct path {
    int row;
    int col;
    int dist;
};

int main() {
    int m,n;
    cin >> m >> n;
    int startr,startc,endr,endc;
    cin >> startr >> startc >> endr >> endc;
    vector<string> grid;
    for(int i = 0; i < m; i++) {
        string row;
        cin >> row;
        grid.push_back(row);
    }
    queue<path> bfs;
    path sp;
    sp.row = startr;
    sp.col = startc;
    sp.dist = 0;
    bfs.push(sp);
    vector< vector<bool> > visited;
    for (int i = 0; i < m; i++) {
        vector<bool> vr;
        for (int j = 0; j < n; j++) {
            vr.push_back(false);
        }
        visited.push_back(vr);
    }
    int md = -1;
    while (!bfs.empty()) {
        path curPath = bfs.front();
        bfs.pop();
      //  cout << "bfs at " << curPath.row << " " << curPath.col << "\n";
        visited[curPath.row][curPath.col] = true;
        if (curPath.row == endr && curPath.col == endc && (md == -1 || curPath.dist < md)) {
            md = curPath.dist;
        }
        if (curPath.row > 0 && grid[curPath.row-1][curPath.col] != '1' && !visited[curPath.row-1][curPath.col]) {
            path np;
            np.row = curPath.row-1;
            np.col = curPath.col;
            np.dist = curPath.dist+1;
            visited[curPath.row-1][curPath.col] = true;
            bfs.push(np);
        }
        if (curPath.col < n-1 && grid[curPath.row][curPath.col+1] != '1' && !visited[curPath.row][curPath.col+1]) {
            path np;
            np.row = curPath.row;
            np.col = curPath.col+1;
            np.dist = curPath.dist+1;
            visited[curPath.row][curPath.col+1] = true;
            bfs.push(np);
        }
        if (curPath.row < m-1 && grid[curPath.row+1][curPath.col] != '1' && !visited[curPath.row+1][curPath.col]) {
            path np;
            np.row = curPath.row+1;
            np.col = curPath.col;
            np.dist = curPath.dist+1;
            visited[curPath.row+1][curPath.col] = true;
            bfs.push(np);
        }
        if (curPath.col > 0 && grid[curPath.row][curPath.col-1] != '1' && !visited[curPath.row][curPath.col-1]) {
            path np;
            np.row = curPath.row;
            np.col = curPath.col-1;
            np.dist = curPath.dist+1;
            visited[curPath.row][curPath.col-1] = true;
            bfs.push(np);
        }
    }
    cout << md << "\n";
    return 0;
}
```

## Test for Python

```python
# test python (sample from offlineimap)
 
class ExitNotifyThread(Thread):
    """This class is designed to alert a "monitor" to the fact that a thread has
    exited and to provide for the ability for it to find out why."""
    def run(self):
        global exitthreads, profiledir
        self.threadid = thread.get_ident()
        try:
            if not profiledir:          # normal case
                Thread.run(self)
            else:
                try:
                    import cProfile as profile
                except ImportError:
                    import profile
                prof = profile.Profile()
                try:
                    prof = prof.runctx("Thread.run(self)", globals(), locals())
                except SystemExit:
                    pass
                prof.dump_stats( \
                            profiledir + "/" + str(self.threadid) + "_" + \
                            self.getName() + ".prof")
        except:
            self.setExitCause('EXCEPTION')
            if sys:
                self.setExitException(sys.exc_info()[1])
                tb = traceback.format_exc()
                self.setExitStackTrace(tb)
        else:
            self.setExitCause('NORMAL')
        if not hasattr(self, 'exitmessage'):
            self.setExitMessage(None)
 
        if exitthreads:
            exitthreads.put(self, True)
 
    def setExitCause(self, cause):
        self.exitcause = cause
    def getExitCause(self):
        """Returns the cause of the exit, one of:
        'EXCEPTION' -- the thread aborted because of an exception
        'NORMAL' -- normal termination."""
        return self.exitcause
    def setExitException(self, exc):
        self.exitexception = exc
    def getExitException(self):
        """If getExitCause() is 'EXCEPTION', holds the value from
        sys.exc_info()[1] for this exception."""
        return self.exitexception
    def setExitStackTrace(self, st):
        self.exitstacktrace = st
    def getExitStackTrace(self):
        """If getExitCause() is 'EXCEPTION', returns a string representing
        the stack trace for this exception."""
        return self.exitstacktrace
    def setExitMessage(self, msg):
        """Sets the exit message to be fetched by a subsequent call to
        getExitMessage.  This message may be any object or type except
        None."""
        self.exitmessage = msg
    def getExitMessage(self):
        """For any exit cause, returns the message previously set by
        a call to setExitMessage(), or None if there was no such message
        set."""
        return self.exitmessage
```

## Test for Bash

```bash
#!/bin/bash
cd $ROOT_DIR
DOT_FILES="lastpass weechat ssh Xauthority"
for dotfile in $DOT_FILES; do conform_link "$DATA_DIR/$dotfile" ".$dotfile"; done
 
# TODO: refactor with suffix variables (or common cron values)
 
case "$PLATFORM" in
    linux)
        #conform_link "$CONF_DIR/shell/zshenv" ".zshenv"
        crontab -l > $ROOT_DIR/tmp/crontab-conflict-arch
        cd $ROOT_DIR/$CONF_DIR/cron
        if [[ "$(diff ~/tmp/crontab-conflict-arch crontab-current-arch)" == ""
            ]];
            then # no difference with current backup
                logger "$LOG_PREFIX: crontab live settings match stored "\
                    "settings; no restore required"
                rm ~/tmp/crontab-conflict-arch
            else # current crontab settings in file do not match live settings
                crontab $ROOT_DIR/$CONF_DIR/cron/crontab-current-arch
                logger "$LOG_PREFIX: crontab stored settings conflict with "\
                    "live settings; stored settings restored. "\
                    "Previous settings recorded in ~/tmp/crontab-conflict-arch."
        fi
    ;;
```

## Test for Haskell

```haskell
{-# LANGUAGE OverloadedStrings #-}
module Main where
 
--import Prelude hiding (id)
--import Control.Category (id)
import Control.Arrow ((>>>), (***), arr)
import Control.Monad (forM_)
-- import Data.Monoid (mempty, mconcat)
 
-- import System.FilePath
 
import Hakyll
 
 
main :: IO ()
main = hakyll $ do
 
    route   "css/*" $ setExtension "css"
    compile "css/*" $ byExtension (error "Not a (S)CSS file")
        [ (".css",  compressCssCompiler)
        , (".scss", sass)
        ]
 
    route   "js/**" idRoute
    compile "js/**" copyFileCompiler
 
    route   "img/*" idRoute
    compile "img/*" copyFileCompiler
 
    compile "templates/*" templateCompiler
 
    forM_ ["test.md", "index.md"] $ \page -> do
        route   page $ setExtension "html"
        compile page $ pageCompiler
            >>> applyTemplateCompiler "templates/default.html"
            >>> relativizeUrlsCompiler
 
sass :: Compiler Resource String
sass = getResourceString >>> unixFilter "sass" ["-s", "--scss"]
                         >>> arr compressCss
```

## Test for PHP

```php

<?php
require_once($GLOBALS['g_campsiteDir']. "/$ADMIN_DIR/country/common.php");
require_once($GLOBALS['g_campsiteDir']. "/classes/SimplePager.php");
camp_load_translation_strings("api");
 
$f_country_language_selected = camp_session_get('f_language_selected', '');
$f_country_offset = camp_session_get('f_country_offset', 0);
if (empty($f_country_language_selected)) {
    $f_country_language_selected = null;
}
$ItemsPerPage = 20;
$languages = Language::GetLanguages(null, null, null, array(), array(), true);
$numCountries = Country::GetNumCountries($f_country_language_selected);
 
$pager = new SimplePager($numCountries, $ItemsPerPage, "index.php?");
 
$crumbs = array();
$crumbs[] = array(getGS("Configure"), "");
$crumbs[] = array(getGS("Countries"), "");
echo camp_html_breadcrumbs($crumbs);
 
?>
 
<?php  if ($g_user->hasPermission("ManageCountries")) { ?>
<table BORDER="0" CELLSPACING="0" CELLPADDING="1">
    <tr>
        <td><a href="add.php"><?php putGS("Add new"); ?></a></td>
    </tr>
</table>
```

## Test for Javascript 

```js
import isTypedArray from 'lodash/isTypedArray';
import reverse from 'lodash/reverse';
import sortBy from 'lodash/sortBy';
import take from 'lodash/take';
import { food101Classes } from './food101';

export function food101topK(classProbabilities, k = 5) {
  const probs = isTypedArray(classProbabilities)
    ? Array.prototype.slice.call(classProbabilities)
    : classProbabilities;

  const sorted = reverse(
    sortBy(
      probs.map((prob, index) => [ prob, index ]),
      probIndex => probIndex[0]
    )
  );

  const topK = take(sorted, k).map(probIndex => {
    const iClass = food101Classes[probIndex[1]];
    return {
      id: probIndex[1],
      name: iClass.replace(/_/, ' '),
      probability: probIndex[0]
    };
  });
  return topK;
};
```

## Test for HTML

```html

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html><head>
<title>A Tiny Page</title>
<style type="text/css">
<!--
      p { font-size:15pt; color:#000 }
    -->
</style></head><!-- real comment -->
<body bgcolor="#FFFFFF" text="#000000" link="#0000CC">
<script language="javascript" type="text/javascript">
      function changeHeight(h) {
        var tds = document.getElementsByTagName("td");
        for(var i = 0; i < tds.length; i++) {
          tds[i].setAttribute("height", h + "px");
      }}
</script>
<h1>abc</h1>
<h2>def</h2>
<p>Testing page</p>
</body></html>
```

## Test for CSS

```css
/*
Monokai style - ported by Luigi Maselli - http://grigio.org
*/

.hljs {
  display: block;
  overflow-x: auto;
  padding: 0.5em;
  background: #272822; color: #ddd;
}

.hljs-tag,
.hljs-keyword,
.hljs-selector-tag,
.hljs-literal,
.hljs-strong,
.hljs-name {
  color: #f92672;
}

.hljs-code {
  color: #66d9ef;
}

.hljs-class .hljs-title {
  color: white;
}
```
