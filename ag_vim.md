
# Extending ag.vim (and ack.vim)

Using **gv** in ag.vim and ack.vim opens a new window on the left side.
Using **go** opens the current item of the search results in the right window.

To extend this behavior, search for the following code:

```
nnoremap <silent> <buffer> H ...
nnoremap <silent> <buffer> o ...
nnoremap <silent> <buffer> t ...
```

- ag.vim: code should be in autoload/ag.vim
- ack.vim: code should be in plugin/ack.vim


Extend the existing code with the following to get new **features**.
- **nl**: open in *new* window (right edge), stay in result
- **nh**: open in *new* window (left edge), stay in result
- **ol**: open in *existing* window (right edge), stay in result
- **oh**: open in *existing* window (left edge), stay in result
- **cl**: close result, jump to window on right edge
- **ch**: close result, jump to window on left edge

```
" <CR> open item in left window
" <C-w><CR> open item in new window
" open in new window (left or right edge), stay in result
exe 'nnoremap <silent> <buffer> nl :let b:height=winheight(0)<CR><C-w><CR><C-w>L:' . l:matches_window_prefix . 'open<CR><C-w>J:exe printf(":normal %d\<lt>c-w>_", b:height)<CR>'
exe 'nnoremap <silent> <buffer> nh :let b:height=winheight(0)<CR><C-w><CR><C-w>H:' . l:matches_window_prefix . 'open<CR><C-w>J:exe printf(":normal %d\<lt>c-w>_", b:height)<CR>'
" open in window on left or right edge, stay in result
exe 'nnoremap <silent> <buffer> ol <CR>:' . l:matches_window_prefix . 'open<CR>'
exe 'nnoremap <silent> <buffer> oh :let b:height=winheight(0)<CR><C-w><Cr><C-w>H<C-w>l<C-w>q:' . l:matches_window_prefix . 'open<CR><C-w>J:exe printf(":normal %d\<lt>c-w>_", b:height)<CR>'
" close result, jump to window on left or right edge
exe 'nnoremap <silent> <buffer> cl <C-w>L:' . l:matches_window_prefix .'close<CR>'
exe 'nnoremap <silent> <buffer> ch <C-w>H:' . l:matches_window_prefix .'close<CR>'
```
