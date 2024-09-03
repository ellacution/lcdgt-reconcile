# Library of Congress Demographic Group Terms OpenRefine Reconciliation Service Endpoint

## About

An OpenRefine reconciliation service for the Library of Congress Demographic Group Terms (LCDGT) available via [id.loc.gov](http://id.loc.gov).

## Run Locally Instructions

Runs directly on localhost:5000 (no /reconcile needed for this recon service)

Before getting started, you'll need Python 3.7 on your computer and be comfortable using LODRefine/OpenRefine/Google Refine.

1. Clone/download/get a copy of this code repository on your computer.
2. In the Command Line Interface, change to the directory where you downloaded this code: `cd directory/with/code/`
3. Install the requirements needed: `pip install -r requirements.txt` (note, I'm updating that to reflect what is currently used - expect bugs + bumps + beautiful mistakes on my part right now).
4. Type in: `python reconcile.py --debug` (you don't need to use debug but this is helpful for knowing what this service is up to while you are working with it).
5. You should see a screen telling you that the service is `Running on http://0.0.0.0:5000/`
6. Leaving that terminal window open and the service running, go start up OpenRefine (however you normally go about it). Open a project in OpenRefine.
7. On the column you would like to reconcile with LCNAF or LCSH (or both), click on the arrow at the top, choose
`Reconcile` > `Start Reconciling...`
8. Click on the `Add Standard Service` button in the bottom left corner.
9. Now enter the URL that the local service is running on - if you've changed nothing in the code, it should be `http://0.0.0.0:5000/`. Click Add Service. If nothing happens upon entering `http://0.0.0.0:5000/`, try `http://localhost:5000/` or `http://127.0.0.1:5000/` instead.
10. You should now be greeted by a list of possible reconciliation types for the LC Reconciliation Service. It takes some fiddling, but you should be able to get the service to work.
11. Click `Start Reconciling` in the bottom right corner.
12. Once finished, you should see the closest options that the LC Services, grouped, found for each cell. You can click on the options and be taken to the id.loc.gov site for that entity's authority. Once you find the appropriate reconciliation choice, click the single arrow box beside it to use that choice just for the one cell, or the double arrows box to use that choice for all other cells containing that text.
13. Once you've got your reconciliation choices done or rejected, you then need to store the LC label and URI (or any subset of those that you want to keep in the data) in your OpenRefine project. This is important:

**Although it appears that you have retrieved your reconciled data into your OpenRefine project, OpenRefine is actually storing the original data still. You need to explicit save the reconciled data in order to make sure it appears/exists when you export your data.**

So, depending on whether or not you wish to keep the original data, you can replace the column with the reconciled data or add a column that contains the reconciled data. I'll do the latter here. On the reconciled data column, click the  arrow at the top, then Choose `Edit Columns` > `Add a new column based on this column`
14. In the GREL box that appears, put the following depending on what you want to pull:

* Label only: `cell.recon.match.name`
* URI: `cell.recon.match.id`
* Label and URI each separated by | (for easier column splitting later): `cell.recon.match.name + " | " + cell.recon.match.id`

When you're down, shut down OpenRefine as you normally would. Go to the terminal where the LC Reconcile service is running and type in cntl + c. This will stop the service. Shut down the terminal window.

## Provenance

This code is a very slightly tweaked version of the [LC reconciliation service](https://github.com/cmharlow/lc-reconcile) by Christina Harlow. Michael Stephens wrote a [demo reconciliation service](https://github.com/mikejs/reconcile-demo) and Ted Lawless wrote a [FAST reconciliation service](https://github.com/lawlesst/fast-reconcile) which that code modifies and builds off of.

All of the access to [id.loc.gov](http://id.loc.gov/) that this OpenRefine Reconciliation service builds off of is
indebted to those who made/make id.loc.gov an option.
