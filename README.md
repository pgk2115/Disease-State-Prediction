# Disease-State-Prediction

The aim of this project is to attempt to build models
which competitively predict a main issue in critical
care analysis: risk of readmission. A variety of exploratory
data analysis, data cleaning, and feature selection has
been performed. Finally, a variety of models have been
fitted to the predictive task, and the
optimal models have been chosen based on varying error
metrics.

## Readmission Prediction

The target outcome in this case represents a readmission after subsequent discharge from
the ICU. This is a binary
classification problem which can be handled with any
classification-based model. Readmission is an important
outcome to predict for several reasons. First, readmission
after discharge represents a significant provider
oversight. If a patient is cleared for discharge then
subsequently readmitted, it represents either an error in
the judgment of the provider or a significant deterioration
in the health of the patient. This mistake can lead to a
variance in the application of care. In turn it can make
resource planning and allocation difficult and can result
in an increase in both expected length of stay and
mortality.

## Data

The MIMIC dataset is a freely
available database comprising deidentified health-related
data associated with over forty thousand patients who
stayed in critical care units of the Beth Israel Deaconess
Medical Center between 2001 and 2012. It is
significantly larger, with 26 comma separated files at a
total size of around 60 gigabytes, and it includes a variety 
of admissions, chart and note data.

## Prediction

Prediction of readmission represents a relatively
challenging task as it
has a generally lower rate of accuracy in literature
review. To predict readmission, the unstructured text
data was utilized. This necessitated some additional data
cleaning and feature engineering. First, the data was
filtered. All elective readmissions were removed, as the
prediction of elective readmission is not the crux of our
motivation. It is desired to predict unplanned
readmission. Next, newborns are removed from the
dataset. Readmission of newborns is indeed a valid
predictive task. However, these cases are highly unique
and require a completely separate analysis and
prediction. Next, all patients who died within the ICU
were removed, as they are unable to be readmitted to the
ICU after death. Then a variable was created which
signified readmission less than 30 days after discharge.
Finally, only the text data consisting of discharge notes
was used. This is because the discharge summary
presumably will contain a complete summary of ICU
stays, including all relevant observations and statistics.
Additionally, it is the most recent chart available.
The dataset is highly imbalanced with regards to
readmissions. There are many more patients who were
not readmitted. Ultimately,
it was decided that under sampling performed optimally.
After this consideration, basic natural language
processing techniques were implemented. Punctuation,
numbers, and names were all removed from the text. The 
language was stemmed using the Porter2 stemmer to
combine similar word roots. Then stop words were
removed. A count vectorizer was used as opposed to a
term frequency inverse document frequency vectorizer,
under the assumption that the common words which may
be weighted by the TFIDF vectorizer may contain
valuable information for the model. Then the training set
was vectorized. Various models were tested, but ultimately 
neural networks outperformed all other baseline models.

Additionally, an RShiny app was built to hold predictions and visualize data <https://pgk2115.shinyapps.io/appp>
