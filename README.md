## Project-SQL---Deforestation

ForestQuery is on a mission to combat deforestation around the world and to raise awareness about this topic and its impact on the environment. The data analysis team at ForestQuery has obtained data from the World Bank that includes forest area and total land area by country and year from 1990 to 2016, as well as a table of countries and the regions to which they belong.
The data analysis team has used SQL to bring these tables together and to query them in an effort to find areas of concern as well as areas that present an opportunity to learn from successes.

Write out a set of recommendations as an analyst on the ForestQuery team.

● What have you learned from the World Bank data?

● Which countries should we focus on over others?

CREATE OR REPLACE VIEW forestation
AS
SELECT f.country_code AS forest_cc,
        f.country_name AS f_name,
        f.year AS f_year,
         f.forest_area_sqkm AS f_sq_km,
         l.total_area_sq_mi AS l_total_area_sq_mi,
         r.region AS r_region, r.income_group AS r_income_group,
          (f.forest_area_sqkm/(l.total_area_sq_mi*2.59))*100 AS perc_forest_area
  FROM forest_area f
  Join land_area l
  ON f.country_code = l.country_code
  JOIN regions r
  ON l.country_code = r.country_code
  WHERE f.year = l.year ORDER BY 1;
