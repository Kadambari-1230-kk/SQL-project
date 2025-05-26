# SQL-project
SELECT 
    T.Date,
    T.BU,
    ISNULL(T.Value, PrevValues.Value) AS Value
FROM HZL_Table T
OUTER APPLY (
    SELECT TOP 1 Value 
    FROM HZL_Table T2
    WHERE T2.BU = T.BU
      AND T2.Date <= T.Date
      AND T2.Value IS NOT NULL
    ORDER BY T2.Date DESC
) AS PrevValues
ORDER BY T.BU, T.Date;
