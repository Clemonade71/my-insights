﻿---
layout: post
title: "March Madness Model"
date: 2025-03-18
categories: [March Madness, Modeling, Basketball]
tags: [NCAA, predictions, analytics]
author: "Aaron Clemons"
---


## Introduction

March Madness. Just the phrase evokes memories of buzzer-beaters, underdog triumphs, and inevitably ruined brackets. Each year, millions of fans eagerly predict the outcome of the NCAA basketball tournament, hoping to find that elusive perfect bracket. Yet, despite years of watching, analyzing, and predicting, March Madness consistently delivers surprises that defy all logic.

But what if we could harness data science to anticipate these surprises? What if statistics could illuminate not only the championship favorites but also the Cinderella stories waiting to unfold?

In this blog post, I’ll walk through how I built my very own statistical model from scratch to forecast the 2025 March Madness tournament outcomes, hopefully identifying top contenders, potential upsets, and highlighting teams poised to capture "One Shining Moment.

## Data Acquisition and Preparation
### Where Did I Get the Data?
My analysis is based primarily on advanced basketball statistics publicly available through sources like KenPom.com and official NCAA/ESPN team databases. 
These sources provide comprehensive team metrics—such as Adjusted Offensive and Defensive Efficiency, Effective Field Goal Percentage, Tempo, Turnover Rate, and much more.
Additionally, historical tournament seeding data from Wikipedia helped set baselines for typical upset frequencies.
To generate a large enough sample size, I've used every NCAA Tournament since 2002.

### Challenges and Data Cleaning
Working with real-world sports data often introduces challenges—missing entries, inconsistent naming conventions, and discrepancies across sources. Here's how I navigated these obstacles:

Missing Data: I used mean imputation to handle missing team statistics, ensuring fairness and completeness without heavily biasing the results.

Standardization: To accurately compare teams, I standardized each metric, converting statistics into comparable scales. This ensured that no single metric unfairly dominated the model simply due to having larger numerical ranges.

Merging datasets: Combining multiple datasets required careful attention to detail. Matching team names across ESPN, KenPom, and NCAA data was crucial, and careful verification was needed to confirm accuracy.
With a clean, consistent dataset ready, I moved forward to build a predictive model aimed at capturing the chaos and excitement of March Madness.

## Building My Model

### Understanding Team Performance (Correlation Analysis)
To accurately predict tournament outcomes, I first needed to identify which statistics correlate most strongly with winning in March Madness. Using a combination of exploratory data analysis and correlation matrices, several key metrics stood out:

Adjusted Offensive Efficiency (points scored per 100 possessions, adjusted for opponent quality)

Adjusted Defensive Efficiency (points allowed per 100 possessions, adjusted similarly)

Effective Field Goal Percentage (eFG%) (a measure of shooting efficiency)

Turnover Rate (TO%) (how frequently a team loses possession)

These metrics amongst others collectively provide a comprehensive snapshot of a team's true ability, beyond surface-level wins and losses.

### Predicting Outcomes (Ridge Regression)
With these insights, I turned to Ridge Regression—a statistical technique perfect for this kind of predictive challenge. 
Ridge Regression is effective because it handles correlated features well and prevents overfitting, ensuring our predictions generalize effectively to the chaos of the tournament.
The Ridge Regression model used the standardized team statistics mentioned above as inputs, with the team's tournament Seed (historically indicative of overall performance and success potential) serving as the outcome variable. 
By training the model on historical tournament data, it learned patterns between team statistics and seeding, providing a reliable measure of relative team strength.

## Key Findings
After running 100,000 tournament simulations, I uncovered some intriguing insights:

# The Top Championship Contenders
While traditional powerhouses made their expected appearances, some surprise contenders emerged prominently from our statistical analysis.

Top Favorites: Florida, Duke, Houston, and Auburn emerged as the statistical front-runners, each having a solid blend of efficiency, shooting accuracy, and defensive discipline.

Balanced Teams Thrive: Teams showing strong balance between offense and defense consistently outperformed those relying heavily on one dimension.

![Top Contenders](/my-insights/assets/images/Contenders.png)
# Identifying Potential Upsets
March Madness wouldn't be March Madness without upsets. By blending my model's predictions with historical upset probabilities, I flagged several early-round games ripe for surprises:

5 vs. 12 Matchups: Colorado State vs. Memphis stood out, with a near-even probability suggesting a tense matchup.

Underestimated Teams: Historical patterns indicate a 40% chance of 12-seeds defeating 5-seeds—our model's blended approach confirmed these matchups as prime upset candidates.

![Upset Alert]({{ site.url }}{{ site.baseurl }}/assets/images/Upsets.png)

How to read this visual:
Teams on the left (low predicted score difference) with higher historical upset probabilities (higher dots) represent the biggest upset risks. 
Warm colors indicate larger seed gaps, highlighting matchups where caution is warranted despite what the predictive model might initially suggest.
Essentially, two seeds within 5 rankings are often the source of upsets, such as 6 vs 11, 7 vs 10, and 8 vs 9 during the first round.

## Cinderella Stories

Who doesn't love a good Cinderella run? To quantify each team's Cinderella potential, I created a custom "Cinderella Index," emphasizing deeper tournament advancement from lower-seeded teams:

# Top Cinderella candidates: 
VCU, New Mexico, Arkansas, Colorado State, and Utah State topped the list, showcasing a strong blend of advanced metrics that suggest they're capable of deep tournament runs despite lower seeds.

![Cinderella Teams](/my-insights/assets/images/Cinderella.png)

## Tournament Heatmap: Visualizing Team Strength
Using a heatmap of advancement probabilities through each round, we clearly see teams poised for deep tournament runs and those likely to bow out early.

![Team Advancement](/my-insights/assets/images/Advance.png)
Darker shades signify stronger probabilities of advancing. Notice how a few select teams have notably consistent colors across multiple rounds—marking them as reliable tournament choices.

These insights and visuals help distill complex predictions into easy-to-understand narratives, whether you're filling out your bracket or just looking for stories to follow during March Madness.

## Challenges & Caveats
While the model provided strong predictions and engaging insights, it’s crucial to recognize some limitations and challenges that arose:

# Data Limitations and Merging Issues
Incomplete Data:
Some teams lacked comprehensive season statistics or had incomplete historical records, requiring me to use imputation methods (like filling missing values with averages). 
This process inherently introduces some bias and uncertainty.

#Matching Teams:
Combining datasets (from ESPN, KenPom, and NCAA official brackets) occasionally posed matching challenges, as different sources sometimes used slightly varied team names or abbreviations. 
I addressed this by manually mapping names.

# Historical vs. Current Team Performance
Historical upset probabilities significantly inform early-round simulations, but the current tournament might differ substantially from past patterns. 
Basketball evolves constantly, and relying heavily on historical probabilities risks overlooking new trends or changing game strategies.

# Limitations of Ridge Regression
Although Ridge Regression handles correlated variables effectively and reduces overfitting, it doesn’t explicitly account for factors such as injuries, team chemistry, or recent momentum, all critical elements in March Madness outcomes.

# Blended Probability Decisions
Due to time constraint, I was unable to go through every single tournament game over the last twenty-three years to find every single win, loss, and upset. Rather I found the upset history of the first round to use as historical verification.
To balance historical trends with statistical modeling, I blended probabilities equally (50% historical, 50% model-based).
While this helped capture both historical context and current data, it introduces a somewhat subjective weighting that may slightly over- or underestimate true upset probabilities.

## Conclusion & Final Thoughts
March Madness predictions are notoriously challenging—even the best statistical models can’t fully tame the madness. 
Still, this exercise provided valuable insights into which teams have the strongest odds, which matchups scream upset alert, and who could write a Cinderella story.
# Key Takeaways:
Balanced teams (strong on both offense and defense) consistently emerge as safer picks.

Historical upset probabilities remain a critical factor—particularly early—but blending these with current team analytics offers superior predictive power.

Lower-seeded teams with strong efficiency metrics (like VCU and New Mexico this year) could potentially surprise brackets.

## For Your Bracket:
Consider including at least one or two 12-over-5 seed upsets.
Favor teams that combine statistical efficiency with historical consistency when choosing late-round teams.
Ultimately, statistical analysis enhances understanding and improves bracket-building strategy, but a bit of March Madness intuition never hurts! 
