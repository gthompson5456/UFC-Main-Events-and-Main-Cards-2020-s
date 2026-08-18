# UFC Main Cards in the 2020s

A Python and Jupyter Notebook project analyzing fighters who competed on the main cards of numbered UFC events from 2020 to the present.

The project focuses exclusively on the UFC’s highest-profile cards. It excludes UFC Fight Night events, preliminary bouts, early prelims, Dana White’s Contender Series, and other MMA promotions.

## Project overview

The notebook downloads and processes UFC event information from ESPN’s public event feed. It identifies numbered UFC events, separates main-card bouts from prelims, and restructures each fight into a fighter-centric analytical dataset.

Each completed bout creates two records:

* One record from the winner’s perspective
* One record from the loser’s perspective

This structure makes it possible to compare fighters, track results over time, calculate win percentages, and create individual fighter drill-downs.

## Project scope

### Included

* Numbered UFC events
* Events from 2020 to the present
* Main-card fights only
* Completed fights
* Male and female fighters
* Three-round and five-round bouts

### Excluded

* UFC Fight Night events
* Preliminary fights
* Early preliminary fights
* Dana White’s Contender Series
* Road to UFC
* The Ultimate Fighter
* Other MMA promotions
* Cancelled fights

UFC Freedom 250 is not included automatically because its name does not follow the standard numbered-event pattern. The notebook includes a configuration option for adding verified special events manually.

## Data source

The project uses the ESPN public UFC event feed for:

* Event names and dates
* Event locations
* Fighter names and IDs
* Fighter records and countries
* Fight results
* Weight classes
* Scheduled rounds
* Ending rounds and times
* Broadcast information
* Bout start times

Downloaded event data is cached by year in `data/raw`. This reduces repeated requests and allows the notebook to reuse previously downloaded data.

## How the project works

The notebook follows this process:

1. Creates the required data and output folders.
2. Downloads or loads cached ESPN UFC event data.
3. Filters the event list to numbered UFC events from 2020 onward.
4. Identifies main-card bouts using each event’s latest scheduled broadcast block.
5. Validates the number of main-card bouts assigned to each event.
6. Applies optional manual card-classification corrections.
7. Creates one analytical record for each fighter in each bout.
8. Calculates point-in-time Elo ratings and expected win probabilities.
9. Produces fighter summaries and interactive Altair charts.
10. Provides fighter and event drill-down tables.
11. Exports dated CSV, HTML, and PNG files.

## Main-card validation

Main-card status is inferred from the scheduled start times contained in the ESPN data.

The notebook flags events with an unusual number of main-card bouts for review. By default, a normal main card is expected to contain between four and six fights.



## Fighter-centric dataset

The main analytical dataset includes fields such as:

* Event name and date
* Fighter and opponent
* Win or loss
* Fighter and opponent countries
* Fighter and opponent records at the event
* Weight class
* Scheduled rounds
* Five-round-bout indicator
* Ending round and time
* Total fight duration
* Pre-fight Elo rating
* Opponent’s pre-fight Elo rating
* Expected win probability
* Post-fight Elo rating
* Elo rating change
* Upset indicator

## Point-in-time Elo ratings

The Elo rating estimates a fighter’s strength based on previous qualifying results and opponent quality.

Ratings rise after wins and fall after losses, with larger changes following unexpected results. “Point-in-time” means each rating uses only information available before that fight and does not use future results.

Every fighter begins with an Elo rating of 1500.

The model is limited to numbered UFC main-card fights from 2020 onward. It does not account for fights before 2020, UFC Fight Night appearances, prelims, or fights in other promotions. Elo results are intended as an analytical feature rather than a betting or prediction model.

## Fighter summaries

The notebook calculates:

* Main-card appearances
* Wins and losses
* Win percentage
* Five-round bouts
* Elo upset victories
* First main-card appearance
* Most recent main-card appearance
* Current Elo rating
* Peak post-fight Elo rating

Win-percentage rankings require a minimum of three qualifying appearances. This prevents fighters with only one fight from automatically appearing at the top of the rankings.

## Visualizations

The project uses Altair because its interactive charts support tooltips, zooming, and exploration.

The notebook creates six visualizations:

1. Most numbered-event main-card wins
2. Best win percentage with at least three appearances
3. Main-card bouts by year
4. Main-card representation by weight class
5. Elo ratings over time
6. Largest Elo upsets

Charts are exported as interactive HTML files and, when `vl-convert-python` is installed, PNG images.

## Fighter and event drill-downs

The fighter drill-down shows every qualifying fight for a selected fighter.

To select a fighter, change:

```python
SELECTED_FIGHTER = "Paddy Pimblett"
```

to another fighter’s name exactly as it appears in the dataset.

The event drill-down defaults to the latest numbered UFC event and displays:

* Winner
* Loser
* Weight class
* Scheduled rounds
* Ending round
* Ending time
* Broadcast

```

The primary packages are:

* pandas
* NumPy
* Requests
* Altair
* vl-convert-python
* Jupyter Notebook

