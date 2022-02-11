---
layout: post
title:  "Digitize and Cluster Research with Xzerpt"
date:   2021-10-27 22:10:00 +0100
categories: jekyll update
tags: research xzerpt thinking-aids
header:
  teaser: "/assets/images/xzerptCard.png"
---

## Xzerpt: a framework for clustering research notes
## Description:

Xzerpt uses idea clustering and source management to bring structure to your research notes and keep track of what ideas you found where. 

Record your ideas in a online interface and then create printable Xzerpt cards you can cluster into stacks on your desk.

Xzerpt is hosted at [xzerpt.com](https://xzerpt.com). 
## Usage

### 1. Data collection

- Conduct research and fill out Xzerpt templates:

  <img src="https://xzerpt.com/exampleImages/xzerptUI.png" alt="UIPicture" width="70%"/>

  - The template contains the following fields:

    - `Type`: _quote_, _paraphrase_, or _own opinion_
    - `Source`: unique name or nickname you keep source details saved under (wherever)
    - `Page`: page number in source (0 for without pages i.e. website)
    - `Topic`: brief summary of idea
    - `Statement`: the idea itself

  - Source details should contain the name/nickname used in the csv and a way to find the source (URL, book title, ISBN, etc):
    ```txt
    Xzerpt
      https://github.com/BrianInGermany/Xzerpt
    brian
      https://github.com/BrianInGermany
    bible
      https://www.bible.com/
    ```
  - Pressing `Cache Card` will add the card to temporary storage. When you're done caching cards, click `Download and Clear Cache` to get your CSV file.
  
  - Caveat: The `|` symbol is the delimiter and using one in the template will break the CSV creation. Substitute them with some other character. 
  
### 2. Card generation

- Click the `Create Cards from CSV` button on the homepage to open the card creator.
- Drag and drop Xzerpt CSVs into the field, and press `Create Cards`:

    <img src="https://xzerpt.com/exampleImages/xzerptcreator.png" alt="cardcreator" width="70%"/>

- Sample output:
  
    <img src="https://xzerpt.com/exampleImages/xzerptCard.png" alt="cardPicture" width="70%"/>

- Print the website using the browser to get your cards
  - Print to A4-size PDF and then print the PDF two-to-a-page for A6 index cards.
  - On A4 size without headers, the cards print two-to-a-page
  

### 3. Card clustering

- Create a coordinate system on your desk with 1, 2, 3, 4 on one axis and A, B, C, D, E on the other. Make it big enough to put one Xzerpt card in each cell.
- Cluster similar Xzerpt cards together. Once two or three cards are in one stack, name the stack. Write down its name on this chart ([pdf link](categoryTable.pdf)):

  [<img src="https://xzerpt.com/exampleImages/categoryTable.png" alt="chartPicture" width="300"/>](https://xzerpt.com/exampleImages/categoryTable.pdf)

- **Rename stacks as often as you like!** The point is to have an appropriate name at the end. You may also want to merge or split stacks as you go.
- When you are finished, you have stacks that represent the low-level structure of your information, like this:

  <img src="https://xzerpt.com/exampleImages/clusterCards.jpg" alt="clusteredCards" width="500"/>

### 4. Stack clustering

- Once you have a set of named stacks on your table, label each stack with a post-it according to your names in the chart.
- Now we're going to cluster the clusters to create a structure for our research!
- Repeat step 3. with a blank chart, this time clustering stacks instead of individual cards and naming these superstacks instead of the stacks.


### 5. Sequentialization

- For each superstack, put its stacks in a logical order. The resulting sequence represents the high-level structure of the information you collected. 
- Optional: For each stack, put its cards in a logical order. This is your low-level structure.
- You should now have one big heap of cards containing ordered superstacks which contain ordered stacks which contain individual cards.
- This is your table of contents!

### 6. Composition

- The final step of the framework is to weave your superstacks, stacks and cards into a new composition. 
- Use ordered superstacks and stacks to write table of contents.
- Put the heap of ordered stacks and superstacks on your desk, and integrate the cards' contents one by one into your paper, presentation or speech.


## Background: Excerpting

The system behind Xzerpt is a type of academic note-taking called excerpting (German: *Exzerpieren*)

   [<img src="https://xzerpt.com/exampleImages/exzerpiren.jpg" alt="exzerpt"/>][1]

- [Taking Notes from Research Reading](https://advice.writing.utoronto.ca/researching/notes-from-research/), University of Toronto
- [How do I excerpt?](https://www.uni-kassel.de/uni/index.php?eID=dumpFile&t=f&f=907&token=57252036805e1227831a802f377dde1c13925dbc), Uni Kassel
- [Ein Exzerpt schreiben](https://www.scribbr.de/studium/exzerpt/), scribbr.de
- [Taking Notes](https://libguides.gatech.edu/c.php?g=54271&p=350393), gatech.edu
- [How to Take Good Notes](https://sites.google.com/site/research4digitalworld/take-notes)

<!-- - [Exzerpieren](https://www.europa-uni.de/de/struktur/zsfl/institutionen/schreibzentrum/angebote/lehrende/materialien/Exzerpieren.pdf), Europa-Uni Frankfurt (Oder)
- [Leitfaden: Ein Exzerpt erstllen](https://mentoren.philol.uni-leipzig.de/fileadmin/mentoren.philol.uni-leipzig.de/uploads/dokumente/Leitfaden_Exzerpt_01.pdf), Uni Leipzig -->

[1]:https://www.uni-erfurt.de/seminarfach/kurs/9/#c67025
