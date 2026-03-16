- Does your proposal include all of the above mentioned sections? 1/1

I appreciated the detailed modeling notebook.

- Are your objectives concrete and do you have a clear stakeholder need? 2/2

I'm really enthusiastic about your plan to bring in information about deployment and it's influence on crime reporting.  If you can get some data, it will be relatively straightforward to determine how much variance is uniquely explained by policing, and 

- Do you have a good data source and have you done a thorough job investigating its provenance and credibility? 1 / 1

- Did you do a thorough job exploring your data 2/2

- Have you done some initial modeling of your problem and do you have some early baseline results?

Nice work with your initial modeling here.  Clearly, a tree based method is going to be a lot better here, because lat / lon will have a non-linear relationship with crime rates.  So you can anticipate substantial improvements.

Note that your clustering approach is another way to accomodate non-linearity.  I would use a density based clustering method, and possibly UMAP - this will give you finer grained clusters.  Once you use clusters to label your data, that label itself can become a feature in you dataset, and you can then use linear or non-linear methods for classification.  But tree-based methods are definitely going to help here.

You've got a bit of a problem with error reporting right now - yes, MAE is low, but I think that is artificially inflating your perceived performance.  This is often the problem with low baseline rate prediction / classification (e.g. disease detection), and so your MAE is telling you, that yes, on average your doing ok because the actual high crime areas are relatively rare.  So, you're going to need to figure out how to address this - it is ultimately a problem of imbalanced data.  

Also note in your modeling - I'm not 100% sure, but it looks to me like your raw data is going to miss cells with *no* crime reported, and so you'll want to complete your dataframe to insert the 0 cells (making sure that you only have cells that are within LA County.). Chances are this isn't a huge problem - most grid cells will have at least one crime.  But it's important to make sure you have complete coverage.


- Do you have a clear path forward 1/1

This is really nice work so far, but you've a lot left to do!  I'm excited to see if you can pull the policing stuff in, so please do what you can to find some data.  It's going to be hard, but there are enough people out there aware of the problem of over-policing that it is likely you'll find something you can work with.

This looks promising: https://direct.mit.edu/rest/article/107/6/1734/117710/Smartphone-Data-Reveal-Neighborhood-Level-Racial

Score: 10/10