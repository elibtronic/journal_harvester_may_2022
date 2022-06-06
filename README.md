# Cross Ref Journal Data Harvester

Downloads all DOIs from Crossref associated with a journal, grabs publisher landing page for article and greps abstract and adds to dataframe. Using Python Notebooks and a library called [habanero](https://habanero.readthedocs.io/en/latest/modules/crossref.html) to query [Crossref API](https://www.crossref.org/documentation/retrieve-metadata/rest-api/) and [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) to do the screen scrapping.

## To Use

* Load up [Harvester](Harvester.ipynb)
* Set `ISSN` & `TITLE`
* Set `SOUP_TAG` and `SOUP_DICT` (examples for T&F and Humanketics included)
* Run All Cells


## Output

Folder called `TITLE` with:

  - long list of html files, grabbed from publisher, all of pattern `$DOI.html`
  - `ISSN_BAD_DOI.txt` - list of DOIs that we couldn't get metadata from. This is usually a DOI used for some pages like 'Thanks Yous' and lists of Editorial boards. (Things that shouldn't have DOIs in other words)
  - `ISSN_bad_html.txt` - similar to above. Records that didn't have Abstracts on them.
  - `ISSN_DOI.txt` - simple list of all DOIs found on CrossRef that match this `ISSN`
  - `TITLE_ISSN.csv` - The **METADATA** of the found journal articles all in one files. Suitable for use as Python Dataframe.

## Example Datasets

Just the final CSV files for brievity

* [ESMQ](ESMQ)
* [JSM](JSM)
* [SMR](SMR)

## EG. Usage

Set the second cell to the following to grab all of SMR on T&F.

```
#JOURNAl TO Grab

#Name of the folder and prefix for our file names
TITLE = "SMR"

#Will be term for CrossRef ISSN search
ISSN = "1441-3523"


#Soup Pattern
#This is the value passed to Beautiful Soup to grab Abstract Text. Different for each Domain

# T & F - soup.find("div",{"class":"abstractSection abstractInFull"}).text
SOUP_TAG = "div"
SOUP_DICT = {"class":"abstractSection abstractInFull"}


# Human Kinetics - soup.find("section",{"class": "abstract"}).text
#SOUP_TAG = "section"
#SOUP_DICT = {"class": "abstract"}

```

## Shout-outs

CrossRef Yo.