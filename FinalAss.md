Skip to content
 
Search…
All gists
Back to GitHub

Sign in
Sign up
Instantly share code, notes, and snippets.

@schinlfc
schinlfc/DB0201EN-PeerAssign-v5.ipynb
Created 11 months ago
0
3
 Code
 Revisions 1
 Forks 3
<script src="https://gist.github.com/schinlfc/9f359e3c6a6f7169f8f6a769605d76b2.js"></script>
Created on Skills Network Labs
 
DB0201EN-PeerAssign-v5.ipynb
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<center>\n",
    "    <img src=\"https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/Logos/organization_logo/organization_logo.png\" width=\"300\" alt=\"cognitiveclass.ai logo\"  />\n",
    "</center>\n",
    "\n",
    "<h1 align=center><font size = 5>Assignment: Notebook for Peer Assignment</font></h1>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Introduction\n",
    "\n",
    "Using this Python notebook you will:\n",
    "\n",
    "1.  Understand three Chicago datasets  \n",
    "2.  Load the three datasets into three tables in a Db2 database\n",
    "3.  Execute SQL queries to answer assignment questions \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Understand the datasets\n",
    "\n",
    "To complete the assignment problems in this notebook you will be using three datasets that are available on the city of Chicago's Data Portal:\n",
    "\n",
    "1.  <a href=\"https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2\">Socioeconomic Indicators in Chicago</a>\n",
    "2.  <a href=\"https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t\">Chicago Public Schools</a>\n",
    "3.  <a href=\"https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2\">Chicago Crime Data</a>\n",
    "\n",
    "### 1. Socioeconomic Indicators in Chicago\n",
    "\n",
    "This dataset contains a selection of six socioeconomic indicators of public health significance and a “hardship index,” for each Chicago community area, for the years 2008 – 2012.\n",
    "\n",
    "A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:\n",
    "[https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2](https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2?cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ&cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ&cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ&cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ)\n",
    "\n",
    "### 2. Chicago Public Schools\n",
    "\n",
    "This dataset shows all school level performance data used to create CPS School Report Cards for the 2011-2012 school year. This dataset is provided by the city of Chicago's Data Portal.\n",
    "\n",
    "A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:\n",
    "[https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t](https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t?cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ&cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ)\n",
    "\n",
    "### 3. Chicago Crime Data\n",
    "\n",
    "This dataset reflects reported incidents of crime (with the exception of murders where data exists for each victim) that occurred in the City of Chicago from 2001 to present, minus the most recent seven days. \n",
    "\n",
    "A detailed description of this dataset and the original dataset can be obtained from the Chicago Data Portal at:\n",
    "[https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2?cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ&cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ)\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Download the datasets\n",
    "\n",
    "This assignment requires you to have these three tables populated with a subset of the whole datasets.\n",
    "\n",
    "In many cases the dataset to be analyzed is available as a .CSV (comma separated values) file, perhaps on the internet. Click on the links below to download and save the datasets (.CSV files):\n",
    "\n",
    "-   <a href=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/data/ChicagoCensusData.csv\" target=\"_blank\">Chicago Census Data</a>\n",
    "\n",
    "-   <a href=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/data/ChicagoPublicSchools.csv\" target=\"_blank\">Chicago Public Schools</a>\n",
    "\n",
    "-   <a href=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/data/ChicagoCrimeData.csv\" target=\"_blank\">Chicago Crime Data</a>\n",
    "\n",
    "**NOTE:** Ensure you have downloaded the datasets using the links above instead of directly from the Chicago Data Portal. The versions linked here are subsets of the original datasets and have some of the column names modified to be more database friendly which will make it easier to complete this assignment.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Store the datasets in database tables\n",
    "\n",
    "To analyze the data using SQL, it first needs to be stored in the database.\n",
    "\n",
    "While it is easier to read the dataset into a Pandas dataframe and then PERSIST it into the database as we saw in Week 3 Lab 3, it results in mapping to default datatypes which may not be optimal for SQL querying. For example a long textual field may map to a CLOB instead of a VARCHAR. \n",
    "\n",
    "Therefore, **it is highly recommended to manually load the table using the database console LOAD tool, as indicated in Week 2 Lab 1 Part II**. The only difference with that lab is that in Step 5 of the instructions you will need to click on create \"(+) New Table\" and specify the name of the table you want to create and then click \"Next\". \n",
    "\n",
    "<img src = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_Coursera_V5/images/LoadingData.png\">\n",
    "\n",
    "##### Now open the Db2 console, open the LOAD tool, Select / Drag the .CSV file for the first dataset, Next create a New Table, and then follow the steps on-screen instructions to load the data. Name the new tables as follows:\n",
    "\n",
    "1.  **CENSUS_DATA**\n",
    "2.  **CHICAGO_PUBLIC_SCHOOLS**\n",
    "3.  **CHICAGO_CRIME_DATA**\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Connect to the database\n",
    "\n",
    "Let us first load the SQL extension and establish a connection with the database\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "%load_ext sql"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "In the next cell enter your db2 connection string. Recall you created Service Credentials for your Db2 instance in first lab in Week 3. From the **uri** field of your Db2 service credentials copy everything after db2:// (except the double quote at the end) and paste it in the cell below after ibm_db_sa://\n",
    "\n",
    "<img src =\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/FinalModule_edX/images/URI.jpg\">\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'Connected: tzf21151@BLUDB'"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Remember the connection string is of the format:\n",
    "# %sql ibm_db_sa://my-username:my-password@my-hostname:my-port/my-db-name\n",
    "# Enter the connection string for your Db2 on Cloud database instance below\n",
    "%sql ibm_db_sa://tzf21151:smswkm7h6d3xl5%5Eg@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Problems\n",
    "\n",
    "Now write and execute SQL queries to solve assignment problems\n",
    "\n",
    "### Problem 1\n",
    "\n",
    "##### Find the total number of crimes recorded in the CRIME table.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>1</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>534</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[(Decimal('534'),)]"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select distinct(count(*)) from CRIME;"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 2\n",
    "\n",
    "##### List community areas with per capita income less than 11000.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>community_area_name</th>\n",
       "            <th>per_capita_income_</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>West Garfield Park</td>\n",
       "            <td>10934</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>South Lawndale</td>\n",
       "            <td>10402</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Fuller Park</td>\n",
       "            <td>10432</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Riverdale</td>\n",
       "            <td>8201</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('West Garfield Park', 10934),\n",
       " ('South Lawndale', 10402),\n",
       " ('Fuller Park', 10432),\n",
       " ('Riverdale', 8201)]"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select community_area_name, per_capita_income_ from chicago_socioeconomic_data where per_capita_income_ < 11000;"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 3\n",
    "\n",
    "##### List all case numbers for crimes  involving minors?\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>case_number</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>HN567387</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>HR391350</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>HM768251</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>HT394616</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('HN567387',), ('HR391350',), ('HM768251',), ('HT394616',)]"
      ]
     },
     "execution_count": 61,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select case_number from crime where primary_type = 'OFFENSE INVOLVING CHILDREN';"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 4\n",
    "\n",
    "##### List all kidnapping crimes involving a child?\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 56,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>primary_type</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>KIDNAPPING</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('KIDNAPPING',)]"
      ]
     },
     "execution_count": 56,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select primary_type from crime where primary_type='KIDNAPPING' and description like '%CHILD%';"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 5\n",
    "\n",
    "##### What kinds of crimes were recorded at schools?\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>name_of_school</th>\n",
       "            <th>primary_type</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>Josephine C Locke Elementary School</td>\n",
       "            <td>CRIMINAL DAMAGE</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Josephine C Locke Elementary School</td>\n",
       "            <td>OTHER OFFENSE</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Abraham Lincoln Elementary School</td>\n",
       "            <td>THEFT</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Abraham Lincoln Elementary School</td>\n",
       "            <td>LIQUOR LAW VIOLATION</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Abraham Lincoln Elementary School</td>\n",
       "            <td>BURGLARY</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('Josephine C Locke Elementary School', 'CRIMINAL DAMAGE'),\n",
       " ('Josephine C Locke Elementary School', 'OTHER OFFENSE'),\n",
       " ('Abraham Lincoln Elementary School', 'THEFT'),\n",
       " ('Abraham Lincoln Elementary School', 'LIQUOR LAW VIOLATION'),\n",
       " ('Abraham Lincoln Elementary School', 'BURGLARY')]"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select name_of_school, primary_type from crime c, schools s\\\n",
    "where c.community_area_number = s.community_area_number limit 5;"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 6\n",
    "\n",
    "##### List the average safety score for all types of schools.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 76,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>Elementary, Middle, or High School</th>\n",
       "            <th>average_safety_score</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>ES</td>\n",
       "            <td>49.520383</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>HS</td>\n",
       "            <td>49.623529</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>MS</td>\n",
       "            <td>48.000000</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>None</td>\n",
       "            <td>None</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('ES', Decimal('49.520383')),\n",
       " ('HS', Decimal('49.623529')),\n",
       " ('MS', Decimal('48.000000')),\n",
       " (None, None)]"
      ]
     },
     "execution_count": 76,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select \"Elementary, Middle, or High School\", avg(safety_score) as average_safety_score from schools group by \"Elementary, Middle, or High School\"; "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 7\n",
    "\n",
    "##### List 5 community areas with highest % of households below poverty line\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 81,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>community_area_name</th>\n",
       "            <th>percent_households_below_poverty</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>Riverdale</td>\n",
       "            <td>56.5</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Fuller Park</td>\n",
       "            <td>51.2</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>Englewood</td>\n",
       "            <td>46.6</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>North Lawndale</td>\n",
       "            <td>43.1</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>East Garfield Park</td>\n",
       "            <td>42.4</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('Riverdale', 56.5),\n",
       " ('Fuller Park', 51.2),\n",
       " ('Englewood', 46.6),\n",
       " ('North Lawndale', 43.1),\n",
       " ('East Garfield Park', 42.4)]"
      ]
     },
     "execution_count": 81,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select community_area_name, percent_households_below_poverty from chicago_socioeconomic_data\\\n",
    "order by percent_households_below_poverty desc nulls last limit 5;"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 8\n",
    "\n",
    "##### Which community area is most crime prone?\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>community_area_number</th>\n",
       "            <th>number_of_crime</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>None</td>\n",
       "            <td>44</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[(None, Decimal('44'))]"
      ]
     },
     "execution_count": 64,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select community_area_number, count(*) as Number_of_Crime from crime group by community_area_number\\\n",
    "order by number_of_crime desc limit 1;"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "jupyter": {
     "source_hidden": true
    }
   },
   "source": [
    "Double-click **here** for a hint\n",
    "\n",
    "<!--\n",
    "Query for the 'community area number' that is most crime prone.\n",
    "-->\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 9\n",
    "\n",
    "##### Use a sub-query to find the name of the community area with highest hardship index\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 68,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>community_area_name</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>Riverdale</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[('Riverdale',)]"
      ]
     },
     "execution_count": 68,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select community_area_name from chicago_socioeconomic_data\\\n",
    "where hardship_index = (select max(hardship_index) from chicago_socioeconomic_data)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Problem 10\n",
    "\n",
    "##### Use a sub-query to determine the Community Area Name with most number of crimes?\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "(ibm_db_dbi.ProgrammingError) ibm_db_dbi::ProgrammingError: Statement Execute Failed: [IBM][CLI Driver][DB2/LINUXX8664] SQL0601N  The name of the object to be created is identical to the existing name \"TZF21151.NUM_CRIME\" of type \"VIEW\".  SQLSTATE=42710 SQLCODE=-601\n",
      "[SQL: create view num_crime as select community_area_number, count(*) as number_of_crime from crime group by community_area_number;]\n",
      "(Background on this error at: http://sqlalche.me/e/13/f405)\n",
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>community_area_number</th>\n",
       "            <th>number_of_crime</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "        <tr>\n",
       "            <td>1</td>\n",
       "            <td>6</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>2</td>\n",
       "            <td>7</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>3</td>\n",
       "            <td>4</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>4</td>\n",
       "            <td>3</td>\n",
       "        </tr>\n",
       "        <tr>\n",
       "            <td>5</td>\n",
       "            <td>4</td>\n",
       "        </tr>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[(1, Decimal('6')),\n",
       " (2, Decimal('7')),\n",
       " (3, Decimal('4')),\n",
       " (4, Decimal('3')),\n",
       " (5, Decimal('4'))]"
      ]
     },
     "execution_count": 25,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql create view num_crime as\\\n",
    "select community_area_number, count(*) as number_of_crime\\\n",
    "from crime group by community_area_number;\n",
    "#num_crime = %sql select community_area_number, count(*) as Number_of_Crime from crime group by community_area_number\n",
    "%sql select * from num_crime limit 5;"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * ibm_db_sa://tzf21151:***@dashdb-txn-sbox-yp-dal09-11.services.dal.bluemix.net:50000/BLUDB\n",
      "Done.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <thead>\n",
       "        <tr>\n",
       "            <th>community_area_name</th>\n",
       "        </tr>\n",
       "    </thead>\n",
       "    <tbody>\n",
       "    </tbody>\n",
       "</table>"
      ],
      "text/plain": [
       "[]"
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%sql select community_area_name from schools s\\\n",
    "    where s.community_area_number = (select community_area_number\\\n",
    "    from num_crime where number_of_crime = (select max(number_of_crime) from num_crime));"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Copyright © 2020 [cognitiveclass.ai](cognitiveclass.ai?utm_source=bducopyrightlink&utm_medium=dswb&utm_campaign=bdu). This notebook and its source code are released under the terms of the [MIT License](https://bigdatauniversity.com/mit-license?cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ&cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ&cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ&cm_mmc=Email_Newsletter-_-Developer_Ed%2BTech-_-WW_WW-_-SkillsNetwork-Courses-IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork-20127838&cm_mmca1=000026UJ&cm_mmca2=10006555&cm_mmca3=M12345678&cvosrc=email.Newsletter.M12345678&cvo_campaign=000026UJ).\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Author(s)\n",
    "\n",
    "<h4> Hima Vasudevan </h4>\n",
    "<h4> Rav Ahuja </h4>\n",
    "<h4> Ramesh Sannreddy </h4>\n",
    "\n",
    "## Contribtuor(s)\n",
    "\n",
    "<h4> Malika Singla </h4>\n",
    "\n",
    "## Change log\n",
    "\n",
    "| Date       | Version | Changed by        | Change Description                             |\n",
    "| ---------- | ------- | ----------------- | ---------------------------------------------- |\n",
    "| 2020-01-15 | 2.2     | Rav Ahuja         | Removed problem 11 and fixed changelog         |\n",
    "| 2020-11-25 | 2.1     | Ramesh Sannareddy | Updated the problem statements, and datasets   |\n",
    "| 2020-09-05 | 2.0     | Malika Singla     | Moved lab to course repo in GitLab             |\n",
    "| 2018-07-18 | 1.0     | Rav Ahuja         | Several updates including loading instructions |\n",
    "| 2018-05-04 | 0.1     | Hima Vasudevan    | Created initial version                        |\n",
    "\n",
    "## <h3 align=\"center\"> © IBM Corporation 2020. All rights reserved. <h3/>\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python",
   "language": "python",
   "name": "conda-env-python-py"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.12"
  },
  "widgets": {
   "state": {},
   "version": "1.1.2"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
 to join this conversation on GitHub. Already have an account? Sign in to comment
© 2022 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
