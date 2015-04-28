### jekyll watching file changes

    jekyll s --force_polling

### access vagrant 4000 port from host system, add this one line to configuration file

    host: 0.0.0.0

### for support GFM, fenced_code_blocks

    markdown: redcarpet
    redcarpet:
      extensions: ["no_intra_emphasis", "fenced_code_blocks", "autolink", "tables", "with_toc_data"]

