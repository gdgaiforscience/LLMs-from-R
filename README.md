# GDG AI for Science - using Large Language Models from R

Join us for a hands-on workshop designed specifically for researchers and students using R that want to leverage AI in their workflows. This workshop will cover the fundamentals of introducing Large Language Model queries into your analysis pipelines.

Expect an intensive session as we work through provided R Scripts to demonstrate typical AI workflows. 

How to use of Large Language Models (LLMs) directly within your R environment.

Join the [GDG AI for Science community](https://gdg.community.dev/events/details/google-gdg-ai-for-science-australia-presents-using-large-language-models-from-r) for talks, events, workshops,  collaborations and more.

Follow along the workshop material: https://gdgaiforscience.github.io/LLMs-from-R/

Or via a Kaggle R notebook: https://www.kaggle.com/code/astrobutter/gdg-ai-for-science-llms-from-r

Or via Google Colab R notebook: https://colab.research.google.com/drive/1GOK7HjrNx5ud5Up4uL0mfCX1Y-ms-99i?usp=sharing


## Developer instructions
Modify `index.qmd` to update the tutorial pages.

Modify `styles.css` and `_quarto.yml` to change the look and feel of the rendered page.

They will be rendered at: https://gdgaiforscience.github.io/LLMs-from-R/



### Setting up this repo for auto-building the github pages site

FYI, this only has to be done once. And has already been done. Now just fork this repo or use it as a template when making a new page!

Build the workshop files locally with 
```
git clone  
cd LLMs-from-R
quarto render index.qmd 
git commit -am "New build"
git push
```

You must also make a `gh-pages` branch and publish the quarto pages to it locally first. Probably better ways to do this:
```
git checkout -n gh-pages
quarto publish gh-pages
git push origin gh-pages 
git checkout main
```

On the repo turn on github pages at: https://github.com/gdgaiforscience/LLMs-from-R/settings/pages
And have it render from `gh-pages` branch.

Add this github action file to render the quarto page on any repo updates. Note any code execution (e.g Python or executable blocks with `{}` syntax will need more installations).
```
name: Quarto Publish

on:
  push:
    branches: main

permissions:
  contents: write
  
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v3

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2
        with:
          tinytex: true

      - name: Publish to GitHub Pages (and render)
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
          path: .
```
