Given this tag:

```
<IncorrectTag with={["peanut", "butter"]} {...andJelly}>Jelly stains!</IncorrectTag>
```

With vim-surround, you can change the whole tag, attributes included, using `cst<CorrectTag><CR>`.

```
<CorrectTag>Jelly stains!</CorrectTag>
```

If you wanted to preserve the attributes, use `cst<CorrectTag<CR>` (without the closing `>` after `CorrectTag`)

```
<CorrectTag with={["peanut", "butter"]} {...andJelly}>Jelly stains!</CorrectTag>
```

Note: This isn't currently repeatable, even with vim-repeat. A repeat will use the tag-eradicating behaviour.