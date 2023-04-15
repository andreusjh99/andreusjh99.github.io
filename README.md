# andreusjh99.github.io

In Progress

Some notes (for myself):

1. Installing Jekyll: https://jekyllrb.com/docs/installation/ubuntu/
2. syntax highlighting for code snippets: `Rouge`
    
    current theme: `monokai`

3. latex for math in md: `MathJax` (refer to `post.html`)
4. jekyll theme
   
    Make sure to specify in `_config.yml`:
    
        theme: jekyll-theme-architect

    and check that the gem is specified in `Gemfile`.

        gem "jekyll-theme-architect", "~> 0.2.0"

    If the gem has not been installed, run 
        
        $ bundle install

5. Referencing one post url from another post:
   
        {% post_url 2021-09-22-automatic-speech-recognition %}

6. Adding css styling to images in markdown:

    A hack to use will be to include your class at the end of your image source like this

        ![alt-text](img-src#your-class)

    Here `img-src` is the image source, i.e. the path to the image.

    In your css, you can then reference the images with the following selector

        img[src$='#your-class'] {
            ...
        }

