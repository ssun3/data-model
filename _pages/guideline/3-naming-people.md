---
title: Naming people
parent: "Standards and conventions"
grand_parent: Guideline
layout: page
nav_order: 1
---


# Naming people

There are three issues related to naming people in a data set; they concern how to name the "entity" (e.g., "participant"), which postfix to use (e.g., "_id") and what format to use for its values (e.g., an integer). We will go over each of this in turn and justify our choice for a particular convention.


## Naming the entity

People who participate in a study and from whom data is collected are typically called "Subjects" or "Participants"; while "subject" has been standard in many subfields of cognitive sciences, "participant" has become more common recently and is considered more respectful to human study participants as it acknowledges their active involvement in the study. Other terms may be common in specific research domains investigating humans (e.g., "respondent", "patient", "child"), non-human animals (e.g., "monkey") or computational models (e.g., "agent"). Still, in other contexts, it might be customary to use more generic terms (e.g., "person", "user"). Finally there are terms that are idiosyncratic to particular data collection services (e.g., "worker").

It is our view that the entity name in the data table should be generic to encompass a large set of use cases (e.g., children, animals, artificial agents) and we therefore second BIDS in the use of "subject" in the data specification and avoid using any other term in the data. This does not mean however that human participants should be addressed as "subjects" in general (for example, when communicating with them or about them); all participants are subjects, but not all subjects are participants (e.g., an AI-agent). Naming a columns or data file using "subject" is convenient and does not imply a disrespect towards study participants.


**Rule #6: Use "subject" to refer to the entity generating the response data. **


## A postfix for the entity and format of the value

A reference to a subject identifier can serve multiple purposes and depending on that purpose a different postfix and format are preferable. The main purposes for a subject identifier are:

purpose #1: ensure the uniqueness of a subject within a study; link all data from a subject within a study. 

purpose #2: select or identify data belonging to a particular subject. For example, if you see an outlier point in a plot and want to understand why that point occurred, it might be necessary to identify that data as belonging to a particular subject and then look in greater detail in that subject’s data.

purpose #3: use the subject's identifier to name their data files.


purpose #4: ensure the uniqueness of a subject across studies. A subject may participate in multiple studies and it might be necessary (e.g., for meta-analyses) to determine whether subjects participated in multiple studies. 

These four purposes have somewhat different requirements. 
P#1 requires uniqueness within a study while P#4 requires uniqueness in general. For P#1 it would suffice to have a participant counter and assign an integer to each participant. But this would not work for P#4. Also while P#4 will typically require long strings to ensure uniqueness, soch long names are impractical for data analysis and storage (P#2, P#3). 

Because of these distinct purposes, we will use two different variables to refer to a subject.


- subject_index: an integer assigned to subjects within a data set, typically but not necessarily in chronological order of starting participation in the study.

- subject_name: a name given to subjects within a data set. Following BIDS recommendations, this name is obtained by converting subject_index to a string and using 0 padding, such that the first subject is named "01". Note that such 0 padding requires knowing how many subjects there are in a study before being able to name them (e.g., if there are less than 100, the first subject would be called "01", but if there are 1000 subjects in total, that subject would be called "0001"). 
We will use a string of length 4 by default as this will most likely cover all of our use cases.

- subject_uuid: a universally unique identifier (UUID), which looks something like: "20025fe6-6868-47c6-a222-a5c06b49c8db". Note that this subject_uuid will not be directly in the L1 Trial data but rather will be stored in a separate table that contains for each subject_name its corresponding subject_uuid.

**Note**: we do not use `*_label` because it does not convey the idea of uniqueness; we do not use "*_ria" (which is obtained by shortening the subjects’s uuid; https://github.com/datalad/git-annex-ria-remote) to avoid potential data privacy issues.