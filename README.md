# test

SELECT
	e.ename
FROM
	employee AS e,
	worksin AS w
WHERE
	w.emp = e.eid
AND w.dept IN (select maxDept from (
	SELECT
		w.dept AS maxDept,
		COUNT (w.emp) AS ENUM
	FROM
		worksin AS w
	GROUP BY
		w.dept
	ORDER BY
		ENUM DESC,
		w.dept DESC
	LIMIT 2
) as topDept)
