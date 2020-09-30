# PariMatch_DataAnalyst

1.1
SELECT CASE
        WHEN COALESCE(Age_groups.group, '') = '' THEN 'NaN' 
        ELSE Age_groups.group
        END AS Age_group,
        SUM(Sum_payment) Total_Expenditures,
        COUNT (DISTINCT (Id_check)) AS Total_Num_operations
FROM
(
    SELECT Id_client, 
           Age, 
           '(' || FLOOR( (age - 1) / 10 ) *10 || '-' || FLOOR( (age + 9) / 10 ) * 10 || ')' 
    AS group FROM Customer_info
) AS Age_groups
INNER JOIN 
Transaction_info
ON Age_groups.Id_client = Transaction_info.Id_client
GROUP BY Age_groups.group
ORDER BY Age_groups.group;