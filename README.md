# CP-theories-SPARQL

## Combining RDF and SPARQL with CP-theories to reason about preferences in a Linked Data setting

Preference representation and reasoning play a central role in supporting users with complex and multi-factorial decision processes. In fact, user tastes can be used to filter information and data in a personalized way, thus maximizing their expected utility. Over the years, many frameworks and languages have been proposed to deal with user preferences. Among them, one of the most prominent formalism to represent and reason with (qualitative) conditional preferences (CPs) are _conditional preference theories_ (_CP-theories_). In this paper, we show how to combine them with Semantic Web technologies in order to encode in a standard SPARQL 1.1 query the semantics of a set of CP statements representing user preferences by means of RDF triples that refer to a _preference_ OWL ontology.  In particular, here we focus on context-uniform conditional (cuc) acyclic CP-theories. The framework that we propose allows a standard SPARQL client to query Linked Data datasets, and to order the results of such queries relative to a set of user preferences. 

Dealing with user preferences is an important aspect of every application designed to provide personalized information to the end-user. The original interest in preferences can be found in decision theory, as a way to support complex, multifactorial decision processes, and nowadays every personalized system needs a preference model to capture what the user likes or dislikes. Once the user model has been represented, it is then exploited to filter information coming from a data source, e.g., a database, in order to provide a ranked list of results matching the order encoded in the preferences of the user.

Here we deal with the much more expressive CP-theories instead of CP-nets. A new extended vocabulary as well as a completely new algorithm to encode CP-theories in SPARQL is proposed. Moreover, an implementation of the overall framework is presented together with experimental evaluations targeted at assessing the users' experience in representing their preferences as CP-theories and the performance of the tool.

## Reference
If you publish research that uses CP-theories-SPARQL please use:
~~~
@article{anellicombining,
  title={Combining RDF and SPARQL with CP-theories to reason about preferences in a Linked Data setting},
  author={Anelli, Vito Walter and De Leone, Renato and Di Noia, Tommaso and Lukasiewicz, Thomas and Rosati, Jessica},
  journal={Semantic Web},
  number={Preprint},
  pages={1--29},
  publisher={IOS Press}
}
~~~

## Experiments
In order to asses the effectiveness of the presented approach and the implemented tool,  we set up two different experiments. 
The first experiment consisted of 20 real users using the tool to express their preferences. After the test, users were asked to fill up a questionnaire (reported in Table 5). We respect the Table numbers from the original paper.  
The dataset adopted consisted of a subset of *DBpedia* 2015-04 related to the four popular domains of: Movies, Food, Music and Books. The statistics of the dataset used for experiments are detailed in Table 3.  
![Table 3](https://github.com/vitowalteranelli/CP-theories-SPARQL/blob/master/imgs/datasetStatistics.png)

It is worth noticing that CP-statements can also be automatically extracted from users data \cite{LIU20137,LIU2015774,KORICHE2010685,6361391}. Nevertheless, we set up the previous experiment to have a hint on the average number of CP-statements $\varphi$  needed to model a user profile as well as on what is, from a user perspective, the most tricky version of $\varphi$ to represent  among:
- T > : x φ > x̂ φ [∅],
- u φ : x φ > x̂ φ [∅],
- u φ : x φ > x̂ φ [W φ ].

The second experiment consisted of simulating 168 users using the platform and expressing an overall number of 6720 preferences and 6720 queries to retrieve the resources ranked by taking into their preferences. The aim of this experiment was that of evaluating the response time of the overall system in retrieving a  list of  resources based on a set of user preferences.

### Test on Real Users
In order to test the capability of a user to exploit the platform and even to test if human users unaware of CP-theories were able to express their preferences, we selected 20 users that did not know anything about CP-theories and, after a 5 minutes tutorial, we asked them to express their preferences by using our tool. We asked them to insert as many preferences as they wanted for each domain on the platform, and we then asked them to fill up a post-experience questionnaire in order to acquire some feedback about the experience. 
The motivation of this experiment is twofold: the first information  that we wanted to collect was the number of preferences that a user is prone to explicitely express. The result for this evaluation is shown in Table \ref{tbl:users_stats}. The users provided an overall number of 322 preferences. The average numbers per user are quite similar among the different domains (between 4 and 6) with a little higher propensity to express preferences over books w.r.t.\ songs. The similar average values, and the similar standard deviations, suggest that  there exists a commonality in the number of expressed preferences over a specific domain.
The second relevant information that we wanted to collect is how much the CP-theories expressiveness may fit a ``natural'' way of expressing preferences by a human being. To this aim, we submitted a small questionnaire with 10 questions whose relative answers in aggregate form are shown in Table \ref{tbl:users_survey} and Fig. \ref{fig:users_survey_q2}. All the questions but Q.2 needed to express a value in a 5-star rating scale, with 1 being the worst answer and 5 the best one.
Users felt that representing preferences was not a trivial operation (3.2 corresponds to the lowest value of the overall questionnaire), but this perceived difficulty is clearly dependent on the type of preference (it is worth to notice that for every specific kind of preference, the score is higher than the overall score). 

Thanks to the survey, we can list in an increasing order of difficulty the different kinds of preferences:

Moreover, if we look at the pie chart in Fig. \ref{fig:users_survey_q2}, it emerges that the most difficult part of the process was to detect the properties (variables $V$) on which the preferences should be expressed. 
Another information that we wanted to collect was if the possible difficulty in expressing preferences is stable or it progressively vanishes as the number of expressed preferences increases. Questions 7, 8 and 9 show that the first preference was quite hard to express, but, as the experience goes on, it becomes much easier reaching an average value of 4.1.

The last relevant information that we wanted to collect is how much the expressiveness of CP-theories  can correspond to a perceived ``natural'' way to express preferences.
Also in this case, the result is interesting, because CP-theories are perceived as a quite good way of expressing preferences with a high value of 3.8.

### Test on Simulated Users

In order to closely simulate the behavior of a real user, we designed a tool able to perform the classical operations of expressing a preference and asking the system for an ordered list of relevant resources.
For each domain of interest, the simulated users randomly extract  (with a uniform distribution) a property that they might be interested in, and then randomly select the other components of the preference (e.g., in case of a simple preference, $\top : x > \hat{x} [\emptyset]$, they select either the more liked resource $x$ and the less liked one $\hat{x}$).
The composed preference is then sent to the server to be processed and stored.
The system checks if the preference produced a cycle, eventually warning the user (in case of a cycle, a new preference is produced).
Once the preference is correctly inserted, the simulated user performs a query to the system to retrieve an ordered list of the 100 most relevant resources. 
The system continues, inserting a new preference for the same domain, and asking the system for a new list. The process ends when 10 preferences are inserted for each domain and the 10 related queries accomplished.  Based on the previous experiment, we considered 10 as a representative number of preferences per user. Fig. \ref{fig:execution} shows the average execution time for an increasing  number of preferences related to the simulated users.\footnote{For those interested in a more fine-grained view of the data, a report of the execution times is publicly available at \url{https://github.com/sisinflab/CP-theories-SPARQL/blob/master/evaluation/evaluationResults.tsv}} The SPARQL engine adopted for the experimental evaluation is Jena Fuseki v. 2.3.1 running on a Linux server (kernel v. 4.4.0-28-generic) with an Intel Xeon @ 2.30GHz CPU and 8 GB RAM, while the local version of DBpedia had been loaded in a Virtuoso Server (v. 07.20.3212), running on a Linux server (kernel v. 4.2.0-23-generic) with an Intel Xeon @ 2.40 GHz CPU and 56 GB RAM. 

The results show that queries based on a number of preferences lower than six take approximately less than one second to return results to the user. This is even more interesting if we consider results of the previous experiments, where we saw that users tend to express an average number of preferences between 4 \mbox{and 6.}

## Credits
This algorithm has been developed by Vito Walter Anelli and Jessica Rosati while working at [SisInf Lab](http://sisinflab.poliba.it) under the supervision of Tommaso Di Noia.  

## Contacts

   Tommaso Di Noia, tommaso [dot] dinoia [at] poliba [dot] it  
   
   Vito Walter Anelli, vitowalter [dot] anelli [at] poliba [dot] it 
