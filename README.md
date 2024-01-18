

## Create tables
```SQL
CREATE TABLE JobOpenings (
    JobID INT PRIMARY KEY,
    JobTitle VARCHAR(255),
    Department VARCHAR(255),
    MinimumExperience INT,
    MinimumEducation VARCHAR(255),
	 MinimumEducationLevel INT
);


CREATE TABLE Applicants (
    ApplicantID INT PRIMARY KEY,
    ApplicantName VARCHAR(255),
    ExperienceYears INT,
    Education VARCHAR(255),  EducationLevel INT,
    AppliedForJobID INT,
    FOREIGN KEY (AppliedForJobID) REFERENCES JobOpenings(JobID)
);
```

## Insert Records
```SQL
INSERT INTO JobOpenings (JobID, JobTitle, Department, MinimumExperience, MinimumEducation, MinimumEducationLevel)
VALUES
(101, 'Spacecraft Pilot', 'Flight Operations', 5, 'Bachelor''s in Aerospace Engineering',1),
(102, 'Mission Specialist', 'Science', 3, 'PhD in Physics or related field',3),
(103, 'Space Engineer', 'Engineering', 3, 'Bachelor''s in Mechanical Engineering',1),
(104, 'Communications Officer', 'Communication', 2, 'Bachelor''s in Communication',1);


INSERT INTO Applicants (ApplicantID, ApplicantName, ExperienceYears, Education,EducationLevel, AppliedForJobID)
VALUES
(501, 'John Astronaut', 7, 'Master''s in Aerospace Engineering',2, 101),
(502, 'Lisa Scientist', 4, 'PhD in Physics', 3,102),
(503, 'Mark Engineer', 5, 'Bachelor''s in Mechanical Engineering',1, 103),
(504, 'Emily Communicator', 3, 'Bachelor''s in Communication',1, 104);
```
 ## 1 List All Job Openings:
-- Retrieve a list of all available job openings, including details about the title, department, minimum experience, and minimum education.
```SQL
SELECT * FROM JobOpenings;
```
## 2. Applicants and Their Jobs:
-- Display the names of applicants and the jobs they have applied for. Include all applicants, even if they haven't applied for any job.
```SQL
SELECT 
    ap.ApplicantName,
    jt.JobTitle AS AppliedForJob
FROM 
    Applicants ap
LEFT JOIN 
    JobOpenings jt ON ap.AppliedForJobID = jt.JobID;
```

 ## 3. Qualified Applicants:
-- Create a report showing the names of applicants who meet or exceed the minimum experience and education requirements for the jobs they have applied for.
```SQL
SELECT 
    ap.ApplicantName,
    jt.JobTitle AS AppliedForJob
FROM 
    Applicants ap
JOIN 
    JobOpenings jt ON ap.AppliedForJobID = jt.JobID
WHERE 
    ap.ExperienceYears >= jt.MinimumExperience
    AND ap.EducationLevel >= jt.MinimumEducationLevel;
```
## 4. Job Applicants Without Match:
-- Identify applicants who have applied for a job that currently has no opening.
```SQL
SELECT
    ap.ApplicantID,
    ap.ApplicantName,
    ap.AppliedForJobID
FROM
    Applicants ap
LEFT JOIN
    JobOpenings jt ON ap.AppliedForJobID = jt.JobID
WHERE
    jt.JobID IS NULL;
```

 ## 5.Experience Range Search:
-- Find all job openings that require a minimum of 3 to 5 years of experience.
-- Experience Range Search
```SQL
SELECT
    *
FROM
    JobOpenings
WHERE
    MinimumExperience BETWEEN 3 AND 5;
```

## 6. Education Level Analysis:
-- Retrieve a list of job titles and the count of applicants who have applied for each job, grouped by education level (e.g., Bachelor's, Master's, PhD).
-- Education Level Analysis
```SQL
SELECT
    J.JobTitle,
    A.EducationLevel,
    COUNT(A.ApplicantID) AS ApplicantCount
FROM
    JobOpenings J
LEFT JOIN
    Applicants A ON J.JobID = A.AppliedForJobID
GROUP BY
    J.JobTitle, A.EducationLevel
ORDER BY
    J.JobTitle, A.EducationLevel;
```


## Sources:
# Table 1: JobOpenings
# Table 2: Applicants

![tablestructure](https://github.com/NootanVijapure/subqueries_part3/assets/30225165/72f6ba1d-dbca-4bc6-aa11-f34cbbf14fb3)

# data entry sample data
![dataentrytable1](https://github.com/NootanVijapure/subqueries_part3/assets/30225165/c91699b4-e1ba-4b55-bd64-f4ac7dbd3417)
![dataentrytable2](https://github.com/NootanVijapure/subqueries_part3/assets/30225165/c6250e16-afa8-402e-81ce-36e5d2c1e626)
