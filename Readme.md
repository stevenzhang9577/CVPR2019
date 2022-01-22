**Updated repository at https://github.com/mattdeitke/CVPR-Accepted-Papers-Viewer**

---

# CVPR 2019 Accepted Papers

The main goal of these scripts is to build a page that displays the accepted papers for CVPR 2019 in a way that is easier for humans to parse (see: https://mattdeitke.com/CVPR-2019). Below is an example of what this repository will display, and following that is what CVPR open access currently shows.

<img src="doc/static/site.gif" style="width:100%"/>
<div style="text-align:center">
	<img src="doc/static/oar_preview.png" style="width:60%;"/>
</div>
In particular, there is functionality to cluster papers based on latent Dirichlet allocation topics, create thumbnail images from the first 8 pages of each PDF, find the abstracts, copy a BibTeX, view the paper and supplementary material, and more. The scripts use Python 3.7 and should work for any past and future CVPR conference (unless they change how they display the pages). Modifications can be made to adapt the format to another conference.

#### Installation

0. Clone this repository `git clone https://github.com/mattdeitke/CVPR2019`

1. Save the HTML from where the accepted papers are displayed. For CVPR, this year, that would be `http://openaccess.thecvf.com/CVPR2019.py`.

2. Run `download_pdfs.py` to download all the PDFs inside the content/ folder. (Note: You will need to point the script from `cvpr2020oar.html` to where ever you saved the HTML files from part 1.)

3. Run `getabstracts.py` to generate the abstract files inside the abstracts/ folder.

4. Install ImageMagick, which can be done using `sudo apt-get install imagemagick` or using another supported method such as `brew install imagemagick`.

5. Run `pdftowordcloud.py` to generate top words for each paper. The output is saved in topwords.p.

6. Run `pdftothumbs.py` to generate tiny thumbnails for all papers. The outputs are saved in thumbs/ folder.

7. Run `scrape.py` to generate each paperid, title, authors list by scraping the cvpr2020oar.html page.

8. Run `makecorpus.py` to create allpapers.txt file that has all papers (one per row).

9. Run `python lda.py -f allpapers.txt -k 7 --alpha=0.5 --beta=0.5 -i 100` . This will generate a pickle file called `ldaphi.p` that contains the LDA word distribution matrix. Thanks to this [nice LDA code](https://github.com/shuyo/iir/blob/master/lda/lda.py) by [@shuyo](https://github.com/shuyo)! It requires nltk library and numpy. In this example we are using 7 categories. You would need to change the `cvprnice_template.html` file a bit if you wanted to try different number of categories.

10. Finally, run `generatenicelda.py` to create the `index.html` page.

### Acknowledgements

Big thanks to [@karpathy](https://github.com/karpathy) for his [NeurIPS preview](https://github.com/karpathy/nipspreview) and [ArXiV Sanity Preserver](https://github.com/karpathy/arxiv-sanity-preserver), which is what this repository builds on! Also a thanks to [@tholman](https://github.com/tholman) for creating a more modern [GitHub Corners](https://github.com/tholman/github-corners) and [@shuyo](https://github.com/shuyo) for the [LDA code](https://github.com/shuyo/iir/blob/master/lda/lda.py)! Finally, more thanks go to the people at CVPR for [openly publishing all of their accepted papers](http://openaccess.thecvf.com/CVPR2019.py)!

#### Licence

MIT License
