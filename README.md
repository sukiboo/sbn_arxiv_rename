# sbn_arxiv_rename
Rename and update papers downloaded from [arXiv.org](https://arxiv.org/).

### What it does
The papers downloaded from arXiv are named according to their identifiers, which might not always be convenient:
```
2001.05530.pdf
1905.06448v2.pdf
1905.10409v2.pdf
```
This script renames them according to the selected naming convention.
Three naming formats are provided in the script (though they can be customized to the user's preference).
##### Format 1 (*default option*): `FirstAuthor_Year_Title.pdf`
Only the first author's last name is used and all the spaces are replaced with underscores, i.e.
```
Dereventsov_2020_Biorthogonal_greedy_algorithms_in_convex_optimization.pdf
Dereventsov_2019_The_Natural_Greedy_Algorithm_for_reduced_bases_in_Banach_spaces.pdf
Dereventsov_2019_Greedy_Shallow_Networks_A_New_Approach_for_Constructing_and_Training_Neural_Networks.pdf
```
##### Format 2: `Authors - Title (Year).pdf`
Only the authors' last names are used and the list of authors is truncated to `FirstAuthor et al.` if there are more than two authors, i.e.
```
Dereventsov, Temlyakov - Biorthogonal greedy algorithms in convex optimization (2020).pdf
Dereventsov, Webster - The Natural Greedy Algorithm for reduced bases in Banach spaces (2019).pdf
Dereventsov et al. - Greedy Shallow Networks: A New Approach for Constructing and Training Neural Networks (2019).pdf
```
##### Format 3: `Authors - Title.pdf`
The list of authors is not truncated and the full names are used, i.e.
```
Anton Dereventsov, Vladimir Temlyakov - Biorthogonal greedy algorithms in convex optimization.pdf
Anton Dereventsov, Clayton Webster - The Natural Greedy Algorithm for reduced bases in Banach spaces.pdf
Anton Dereventsov, Armenak Petrosyan, Clayton Webster - Greedy Shallow Networks: A New Approach for Constructing and Training Neural Networks.pdf
```

### How it works
##### Forming a new name
The script extracts the arxiv identifier from either the file's name or metadata and uses it to retrieve the paper's metadata (authors, title, year) from [arXiv.org](https://arxiv.org/), which is used to rename the paper according to the selected naming format.
##### Updating a paper
Optionally, the script can update the papers to their latest versions.
If the option `paper_update` is set to `True` (*default*), the most recent version of the paper will be downloaded from arXiv.
##### Paper renaming and copying
The renamed papers are copied to the destination folder (*defaults to* `./arxiv_papers/`), while the original pdf files are left intact.
##### Metadata changing
The script adds `/arxiv_id` and `/updated` fields to every renamed paper's metadata so that those papers are recognized later regardless of their names.
##### If something went wrong
If the metadata for a paper was not obtained (e.g. due to incorrect arxiv identifier or corrupted metadata) the file is copied to the destination folder 'as is', i.e. without metadata changes or renaming.

### How to run it
First, install the requirements specified in `requirements.txt`, e.g.
```
pip install -r requirements.txt
```
Then just drop the file `sbn_arxiv_rename.py` into the folder with the arxiv papers and run it with Python, i.e.
```
python sbn_arxiv_rename.py
```
The folder `arxiv_papers` will be created with the renamed/updated papers copied to it.
The original pdf files are not changed and are left exactly where they were.

Note that papers already processed by the script contain `/arxiv_id` and `/updated` fields in the metadata and thus can be run through the script again at any point for the purpose of renaming and/or updating.

### License
This project is licensed under the [MIT License](https://mit-license.org/).
