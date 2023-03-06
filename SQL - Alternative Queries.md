## Draw the triangle - 1
P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):
### Input Format
* * * * * 
* * * * 
* * * 
* * 
*

```sql
DROP PROCEDURE IF EXISTS `DoPattern`;
DELIMITER $$
CREATE PROCEDURE DoPattern()
BEGIN
    DECLARE CT INT(10) DEFAULT 20;
    DECLARE CH VARCHAR(256) DEFAULT " *";
    CREATE TEMPORARY TABLE `pattern` (`rowno` INT(2) UNSIGNED, `pattern_string` VARCHAR(50)) ENGINE=MEMORY;

    WHILE CT > 0 DO
        INSERT INTO `pattern` (`rowno`,`pattern_string`) VALUES (CT,REPEAT(CH,CT));
        SET CT = CT - 1;
    END WHILE;

    SELECT `pattern_string` FROM `pattern` ORDER BY `rowno` DESC;
    DROP TABLE `pattern`;
END$$
DELIMITER ;

CALL DoPattern();
```

## Draw the triangle - 2
P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):

* 
* * 
* * * 
* * * * 
* * * * *
Write a query to print the pattern P(20).

``sql
set @number = 0;
select repeat('* ', @number := @number + 1) 
from information_schema.tables
where @number < 20 ``


## Draw the triangle - 2
Write a query to print all prime numbers less than or equal to 1000. Print your result on a single line, and use the ampersand (&) character as your separator (instead of a space).

For example, the output for all prime numbers <= 10 would be:

```DELIMITER //
CREATE PROCEDURE FIND_PRIME(num INT)
BEGIN
    DECLARE output VARCHAR(1000) DEFAULT '2';
    DECLARE n, i, is_prime INT;

    IF (num >= 3) THEN
        SET n := 3;
        WHILE (n <= num) DO
            SET i := 2;
            SET is_prime := 1;
            
             WHILE i <= CEIL(SQRT(n)) DO
                IF n % i = 0 THEN 
                    SET is_prime := 0; 
                END IF; 
                SET i := i + 1;
            END WHILE; 

            IF (is_prime = 1) THEN
                SET output := CONCAT_WS('&', output, n);
            END IF;

            SET n := n + 1;
        END WHILE;
    END IF;
    SELECT output;
END; //

CALL FIND_PRIME(1000); ```
