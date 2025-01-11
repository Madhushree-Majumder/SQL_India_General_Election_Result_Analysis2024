# SQL_India_General_Election_Result_Analysis2024_Project
## Project Overview

### Project Title: India's_General_Election_Result_Analysis_2024
### Level: Advanced
### Database:[constituencywise_details.csv][constituencywise_results.csv][partywise_results.csv][states.csv][statewise_results.csv]
**This Project is designed to demonstrate SQL skills and techniques typically used to data analysts to explore, clean, and analyze 2024 election result data. The project involves setting up a general election database and performing exploratory data analysis (EDA), and answering business questions through SQL quaries. This project is ideal for those who are starting thier journey in data analysis and to build a solid foundation in SQL.

## Objectives
**1. Set up a Election Analysis Database: Create an election analysis database with the provided election data.
**2. Exploratory Data Analysis(EDA): Perform basic explaratory data analysis to understand the dataset.
**3. Business Analysis: Use SQL to answer specific business questions and derive insights from the election data.

## Project Structure
###1. Database Setup
       Database Creation:The project starts by creating a database named [India_Election_Results]
       Table Creation: Tables named constituencywise_details, constituencywise_results, partywise_results,statewise_results,states are created to store election result data.
###2. Data Analysis and Findings
       The following SQL queries were developed to answer specific business questions:

1. **Total Seats
   
   ''' sql
	SELECT 
	DISTINCT COUNT (Parliament_Constituency) AS Total_Seats
	FROM constituencywise_results
 
'''
2. **What is the total number of seats available for elections in each state

   ''' sql
SELECT 
    s.State AS State_Name,
    COUNT(cr.Constituency_ID) AS Total_Seats_Available
FROM 
    constituencywise_results cr
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN 
    states s ON sr.State_ID = s.State_ID
GROUP BY 
    s.State
ORDER BY 
    s.State;
'''
    
3.**Total Seats Won by NDA Allianz

''' sql
SELECT 
    SUM(CASE 
            WHEN party IN (
                'Bharatiya Janata Party - BJP', 
                'Telugu Desam - TDP', 
				'Janata Dal  (United) - JD(U)',
                'Shiv Sena - SHS', 
                'AJSU Party - AJSUP', 
                'Apna Dal (Soneylal) - ADAL', 
                'Asom Gana Parishad - AGP',
                'Hindustani Awam Morcha (Secular) - HAMS', 
                'Janasena Party - JnP', 
				'Janata Dal  (Secular) - JD(S)',
                'Lok Janshakti Party(Ram Vilas) - LJPRV', 
                'Nationalist Congress Party - NCP',
                'Rashtriya Lok Dal - RLD', 
                'Sikkim Krantikari Morcha - SKM'
            ) THEN [Won]
            ELSE 0 
        END) AS NDA_Total_Seats_Won
FROM 
    partywise_results

'''

4. **Seats Won by NDA Allianz Parties
   
   ''' sql
SELECT 
    party as Party_Name,
    won as Seats_Won
FROM 
    partywise_results
WHERE 
    party IN (
        'Bharatiya Janata Party - BJP', 
        'Telugu Desam - TDP', 
		'Janata Dal  (United) - JD(U)',
        'Shiv Sena - SHS', 
        'AJSU Party - AJSUP', 
        'Apna Dal (Soneylal) - ADAL', 
        'Asom Gana Parishad - AGP',
        'Hindustani Awam Morcha (Secular) - HAMS', 
        'Janasena Party - JnP', 
		'Janata Dal  (Secular) - JD(S)',
        'Lok Janshakti Party(Ram Vilas) - LJPRV', 
        'Nationalist Congress Party - NCP',
        'Rashtriya Lok Dal - RLD', 
        'Sikkim Krantikari Morcha - SKM'
    )
ORDER BY Seats_Won DESC
 '''

5. **Total Seats Won by I.N.D.I.A. Allianz
   
   ''' sql
SELECT 
    SUM(CASE 
            WHEN party IN (
                'Indian National Congress - INC',
                'Aam Aadmi Party - AAAP',
                'All India Trinamool Congress - AITC',
                'Bharat Adivasi Party - BHRTADVSIP',
                'Communist Party of India  (Marxist) - CPI(M)',
                'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                'Communist Party of India - CPI',
                'Dravida Munnetra Kazhagam - DMK',
                'Indian Union Muslim League - IUML',
                'Nat`Jammu & Kashmir National Conference - JKN',
                'Jharkhand Mukti Morcha - JMM',
                'Jammu & Kashmir National Conference - JKN',
                'Kerala Congress - KEC',
                'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                'Rashtriya Janata Dal - RJD',
                'Rashtriya Loktantrik Party - RLTP',
                'Revolutionary Socialist Party - RSP',
                'Samajwadi Party - SP',
                'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                'Viduthalai Chiruthaigal Katchi - VCK'
            ) THEN [Won]
            ELSE 0 
        END) AS INDIA_Total_Seats_Won
FROM 
    partywise_results

'''

6.** Seats Won by I.N.D.I.A. Allianz Parties

   '''sql
SELECT 
    party as Party_Name,
    won as Seats_Won
FROM 
    partywise_results
WHERE 
    party IN (
        'Indian National Congress - INC',
                'Aam Aadmi Party - AAAP',
                'All India Trinamool Congress - AITC',
                'Bharat Adivasi Party - BHRTADVSIP',
                'Communist Party of India  (Marxist) - CPI(M)',
                'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                'Communist Party of India - CPI',
                'Dravida Munnetra Kazhagam - DMK',
                'Indian Union Muslim League - IUML',
                'Nat`Jammu & Kashmir National Conference - JKN',
                'Jharkhand Mukti Morcha - JMM',
                'Jammu & Kashmir National Conference - JKN',
                'Kerala Congress - KEC',
                'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                'Rashtriya Janata Dal - RJD',
                'Rashtriya Loktantrik Party - RLTP',
                'Revolutionary Socialist Party - RSP',
                'Samajwadi Party - SP',
                'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                'Viduthalai Chiruthaigal Katchi - VCK'
    )
ORDER BY Seats_Won DESC
 '''

7. **Add new column field in table partywise_results to get the Party Allianz as NDA, I.N.D.I.A and OTHER
   
   ''' sql
ALTER TABLE partywise_results
ADD party_alliance VARCHAR(50);
I.N.D.I.A Allianz
UPDATE partywise_results
SET party_alliance = 'I.N.D.I.A'
WHERE party IN (
    'Indian National Congress - INC',
    'Aam Aadmi Party - AAAP',
    'All India Trinamool Congress - AITC',
    'Bharat Adivasi Party - BHRTADVSIP',
    'Communist Party of India  (Marxist) - CPI(M)',
    'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
    'Communist Party of India - CPI',
    'Dravida Munnetra Kazhagam - DMK',	
    'Indian Union Muslim League - IUML',
    'Jammu & Kashmir National Conference - JKN',
    'Jharkhand Mukti Morcha - JMM',
    'Kerala Congress - KEC',
    'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
    'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
    'Rashtriya Janata Dal - RJD',
    'Rashtriya Loktantrik Party - RLTP',
    'Revolutionary Socialist Party - RSP',
    'Samajwadi Party - SP',
    'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
    'Viduthalai Chiruthaigal Katchi - VCK'
);
NDA Allianz
UPDATE partywise_results
SET party_alliance = 'NDA'
WHERE party IN (
    'Bharatiya Janata Party - BJP',
    'Telugu Desam - TDP',
    'Janata Dal  (United) - JD(U)',
    'Shiv Sena - SHS',
    'AJSU Party - AJSUP',
    'Apna Dal (Soneylal) - ADAL',
    'Asom Gana Parishad - AGP',
    'Hindustani Awam Morcha (Secular) - HAMS',
    'Janasena Party - JnP',
    'Janata Dal  (Secular) - JD(S)',
    'Lok Janshakti Party(Ram Vilas) - LJPRV',
    'Nationalist Congress Party - NCP',
    'Rashtriya Lok Dal - RLD',
    'Sikkim Krantikari Morcha - SKM'
);
OTHER
UPDATE partywise_results
SET party_alliance = 'OTHER'
WHERE party_alliance IS NULL;
'''


8. **Which party alliance (NDA, I.N.D.I.A, or OTHER) won the most seats across all states?
   
   ''' sql
SELECT 
    p.party_alliance,
    COUNT(cr.Constituency_ID) AS Seats_Won
FROM 
    constituencywise_results cr
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
WHERE 
    p.party_alliance IN ('NDA', 'I.N.D.I.A', 'OTHER')
GROUP BY 
    p.party_alliance
ORDER BY 
    Seats_Won DESC;

'''
9.** Winning candidate's name, their party name, total votes, and the margin of victory for a specific state and constituency?

''' sql
SELECT cr.Winning_Candidate, p.Party, p.party_alliance, cr.Total_Votes, cr.Margin, cr.Constituency_Name, s.State
FROM constituencywise_results cr
JOIN partywise_results p ON cr.Party_ID = p.Party_ID
JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN states s ON sr.State_ID = s.State_ID
WHERE s.State = 'Uttar Pradesh' AND cr.Constituency_Name = 'AMETHI';
 '''
 
10.**What is the distribution of EVM votes versus postal votes for candidates in a specific constituency?

''' sql
SELECT 
    cd.Candidate,
    cd.Party,
    cd.EVM_Votes,
    cd.Postal_Votes,
    cd.Total_Votes,
    cr.Constituency_Name
FROM 
    constituencywise_details cd
JOIN 
    constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
WHERE 
    cr.Constituency_Name = 'MATHURA'
ORDER BY cd.Total_Votes DESC;
 '''

11. **Which parties won the most seats in s State, and how many seats did each party win?
    
''' sql
SELECT 
    p.Party,
    COUNT(cr.Constituency_ID) AS Seats_Won
FROM 
    constituencywise_results cr
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN states s ON sr.State_ID = s.State_ID
WHERE 
    s.state = 'Andhra Pradesh'
GROUP BY 
    p.Party
ORDER BY 
    Seats_Won DESC;
 '''

12.**What is the total number of seats won by each party alliance (NDA, I.N.D.I.A, and OTHER) in each state for the India Elections 2024?

''' sql
SELECT 
    s.State AS State_Name,
    SUM(CASE WHEN p.party_alliance = 'NDA' THEN 1 ELSE 0 END) AS NDA_Seats_Won,
    SUM(CASE WHEN p.party_alliance = 'I.N.D.I.A' THEN 1 ELSE 0 END) AS INDIA_Seats_Won,
	SUM(CASE WHEN p.party_alliance = 'OTHER' THEN 1 ELSE 0 END) AS OTHER_Seats_Won
FROM 
    constituencywise_results cr
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN 
    states s ON sr.State_ID = s.State_ID
WHERE 
    p.party_alliance IN ('NDA', 'I.N.D.I.A',  'OTHER')  -- Filter for NDA and INDIA alliances
GROUP BY 
    s.State
ORDER BY 
    s.State;
'''
 

13.** Which candidate received the highest number of EVM votes in each constituency (Top 10)?

''' sql
SELECT TOP 10
    cr.Constituency_Name,
    cd.Constituency_ID,
    cd.Candidate,
    cd.EVM_Votes
FROM 
    constituencywise_details cd
JOIN 
    constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
WHERE 
    cd.EVM_Votes = (
        SELECT MAX(cd1.EVM_Votes)
        FROM constituencywise_details cd1
        WHERE cd1.Constituency_ID = cd.Constituency_ID
    )
ORDER BY 
    cd.EVM_Votes DESC;

 '''
14. **Which candidate won and which candidate was the runner-up in each constituency of State for the 2024 elections?
    
'''sql
WITH RankedCandidates AS (
    SELECT 
        cd.Constituency_ID,
        cd.Candidate,
        cd.Party,
        cd.EVM_Votes,
        cd.Postal_Votes,
        cd.EVM_Votes + cd.Postal_Votes AS Total_Votes,
        ROW_NUMBER() OVER (PARTITION BY cd.Constituency_ID ORDER BY cd.EVM_Votes + cd.Postal_Votes DESC) AS VoteRank
    FROM 
        constituencywise_details cd
    JOIN 
        constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
    JOIN 
        statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
    JOIN 
        states s ON sr.State_ID = s.State_ID
    WHERE 
        s.State = 'Maharashtra'
)

SELECT 
    cr.Constituency_Name,
    MAX(CASE WHEN rc.VoteRank = 1 THEN rc.Candidate END) AS Winning_Candidate,
    MAX(CASE WHEN rc.VoteRank = 2 THEN rc.Candidate END) AS Runnerup_Candidate
FROM 
    RankedCandidates rc
JOIN 
    constituencywise_results cr ON rc.Constituency_ID = cr.Constituency_ID
GROUP BY 
    cr.Constituency_Name
ORDER BY 
    cr.Constituency_Name;
'''

** Query Explaination:
**1. Common Table Expression (CTE) RankedCandidates
**•	WITH RankedCandidates AS: This section creates a Common Table Expression (CTE) named RankedCandidates, which is used to rank candidates based on their total votes within each constituency.
**•	SELECT ... FROM constituencywise_details cd: This part of the CTE retrieves data from the constituencywise_details table, including:
**o	cd.Constituency_ID: The ID of the constituency.
**o	cd.Candidate: The name of the candidate.
**o	cd.Party: The party of the candidate.
**o	cd.EVM_Votes: The number of EVM votes received by the candidate.
**o	cd.Postal_Votes: The number of postal votes received by the candidate.
**o	cd.EVM_Votes + cd.Postal_Votes AS Total_Votes: The total votes received by the candidate (sum of EVM and postal votes).
**•	ROW_NUMBER() OVER (PARTITION BY cd.Constituency_ID ORDER BY cd.EVM_Votes + cd.Postal_Votes DESC) AS VoteRank:
**o	ROW_NUMBER() is a window function that assigns a unique rank to each candidate within their respective constituency.
**o	PARTITION BY cd.Constituency_ID ensures that the ranking is done separately for each constituency.
**o	ORDER BY cd.EVM_Votes + cd.Postal_Votes DESC orders candidates by their total votes in descending order, so the candidate with the most votes gets rank 1.
**•	JOIN ... ON ...: Joins are performed to combine information from related tables:
**o	constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
**o	statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
**o	states s ON sr.State_ID = s.State_ID
**•	WHERE s.State = 'Maharashtra': Filters the results to include only data related to the state of Maharashtra.
**2. Main Query
**•	SELECT ... FROM RankedCandidates rc: The main query retrieves data from the RankedCandidates CTE to find the winning and runner-up candidates for each constituency.
**•	MAX(CASE WHEN rc.VoteRank = 1 THEN rc.Candidate END) AS Winning_Candidate:
**o	CASE WHEN rc.VoteRank = 1 THEN rc.Candidate END selects the candidate with the highest vote rank (rank 1) for each constituency.
**o	MAX(...) ensures that only one candidate is selected for each constituency.
**•	MAX(CASE WHEN rc.VoteRank = 2 THEN rc.Candidate END) AS Runnerup_Candidate:
**o	CASE WHEN rc.VoteRank = 2 THEN rc.Candidate END selects the candidate with the second highest vote rank (rank 2) for each constituency.
**o	MAX(...) ensures that only one candidate is selected for each constituency.
**•	JOIN ... ON ...: Joins the RankedCandidates CTE with the constituencywise_results table to get the constituency names.
**•	GROUP BY cr.Constituency_Name: Groups the results by constituency name to ensure that the winning and runner-up candidates are determined for each constituency.
**•	ORDER BY cr.Constituency_Name: Orders the results alphabetically by constituency name for easier readability.

 

15. **For the state of Maharashtra, what are the total number of seats, total number of candidates, total number of parties, total votes (including EVM and postal), and the breakdown of EVM and postal votes?
    
    ''' sql
SELECT 
    COUNT(DISTINCT cr.Constituency_ID) AS Total_Seats,
    COUNT(DISTINCT cd.Candidate) AS Total_Candidates,
    COUNT(DISTINCT p.Party) AS Total_Parties,
    SUM(cd.EVM_Votes + cd.Postal_Votes) AS Total_Votes,
    SUM(cd.EVM_Votes) AS Total_EVM_Votes,
    SUM(cd.Postal_Votes) AS Total_Postal_Votes
FROM 
    constituencywise_results cr
JOIN 
    constituencywise_details cd ON cr.Constituency_ID = cd.Constituency_ID
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN 
    states s ON sr.State_ID = s.State_ID
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
WHERE 
    s.State = 'Maharashtra';
 
'''
## Findings
543 total seats are there. NDA won 292 seats, BJP won highest seats in NDA Alliance, I.N.D.I.A Alliance won 234 seats, INC (Indian National Congress) won highest seats in I.N.D.I.A Alliance.
Party, total_votes,margin, state, Constituency Name wise winning candidates name, specific constituencywise distribution of EVM votes versus Postal votes for candidates, statewise seats won by each party, top 10 highest candidates details, constituencywise winning and runner up candidate names.

## Reports
A detailed report summarizing total seats in each state, Total number of seats won by each parties, Statewise winning seats for each party, winning candidate's all information, top vote receiving candidate, statewise winner and runner-up information. 
## Conclusion
This project serve as a comprehensive introduction to SQL for data analysts, covering database setup, exploratory data analysis and business-driven SQL quaries. The findings from this project can help drive election result decisions by understanding candidate details and party perfomance.
