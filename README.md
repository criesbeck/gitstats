This tool analyzes **git log** output to identify potential team and bus factor issues for small
developer teams. 

# Usage

Prepare a git log file and save it somewhere convenient.

```
git log --no-merges --name-status main > ~/gitlog.txt
```

Put the output file some place easy to find outside your repository. The command above stores the output in 
your home directory. 

Upload the output file to https://criesbeck.github.io/gitstats/ for analysis. Analysis is done
in the browser. Nothing is passed to or saved on the server.

# User renaming

Optionally, you can upload a JSON file to replace git usernames with real names. The JSON file should 
map git usernames to real names, e.g.,

```
{
  "jsmith": "John",
  "jdoe": "Jane"
}
```

This can also be used to handle situations where a team member has submitted until several git usernames.

# Output

After uploading, the app displays the following tables. 

## Commits

The Commits table summarizes commits
per week by each team member since the start of the project. This is comparable to
the **Contributors** section of the **Insight**
page of the repo on Github, except that 
- delete commits are not counted
- the dates are the end of each week, e.g., the column **3/6/2022** would count
the commits for the week ending on March 6, 2022. 

Commits are not a measure of work or value. Some commits are trivial, some are major.
But a team should always be concerned about their processes 
when there are team members with fewer than two commits
in a week.

## Collaborations

If the commits include ``co-authored-by`` trailers, the Collaborations table shows how many times each pair of developers has collaborated on a commit. The first entry on each row is how often the developer worked alone. The other entries are how often the developer worked with each of the other developers.

This is a measure of how much the team is working together. Teams should focus on 
pairs of developers who have not collaborated at all or only a few times. 

Co-author data can be added to commits using 
[Live Share](https://www.ssw.com.au/rules/co-authored-commits) in VS Code, with the 
[git-mob](https://marketplace.visualstudio.com/items?itemName=RichardKotze.git-mob)
VS Code extension, or with 
[the **git commit** command](https://docs.github.com/en/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/creating-a-commit-with-multiple-authors).


## Bus factor

The second table displays how often each developer has contributed to each code file. 
Code file means JavaScript, CSS, HTML, or YAML.
Most active files are listed first. Activity is based on number and recency of edits.
The cells of the table show what percentage each developer contributed to the activity on each file.

Developers who have contributed less than 5% to a file are highlighted. 
These developers should be first in line for future work on those files.

Active files with only one or two contributors over 5% are 
bus factor risks and are highlighted. Pay particular attention to bus factor
issues in the top ten or so file. 

Future work on those files should include other team members.

# Customization

Clone this repository. 

To change what files are tracked, edit the regular expressions in  **EDIT_PAT**.

To change the threshold for being an active contributor, change **THRESHOLD**.