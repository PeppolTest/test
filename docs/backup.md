# Database Backup – Schema `aston`

This file contains the full MySQL Workbench forward engineering script for the `aston` schema.  
It can be used to recreate the database structure when needed.

---

## Full SQL Script

```sql
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
-- -----------------------------------------------------
-- Schema aston
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema aston
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `aston` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci ;
USE `aston` ;

-- -----------------------------------------------------
-- Table `aston`.`t_event`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `aston`.`t_event` (
  `pk_event` INT NOT NULL AUTO_INCREMENT,
  `description` VARCHAR(200) NULL DEFAULT NULL,
  `event_name` VARCHAR(45) NOT NULL,
  `event_date` DATETIME NOT NULL,
  PRIMARY KEY (`pk_event`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `aston`.`t_location`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `aston`.`t_location` (
  `pk_location` INT NOT NULL AUTO_INCREMENT,
  `zip_code` VARCHAR(45) CHARACTER SET 'utf8mb4' COLLATE 'utf8mb4_0900_ai_ci' NULL DEFAULT NULL,
  `location` TEXT CHARACTER SET 'utf8mb4' COLLATE 'utf8mb4_0900_ai_ci' NULL DEFAULT NULL,
  `country` TEXT CHARACTER SET 'utf8mb4' COLLATE 'utf8mb4_0900_ai_ci' NULL DEFAULT NULL,
  `main_municipality` TEXT CHARACTER SET 'utf8mb4' COLLATE 'utf8mb4_0900_ai_ci' NULL DEFAULT NULL,
  `province` TEXT CHARACTER SET 'utf8mb4' COLLATE 'utf8mb4_0900_ai_ci' NULL DEFAULT NULL,
  PRIMARY KEY (`pk_location`))
ENGINE = InnoDB
AUTO_INCREMENT = 2765
DEFAULT CHARACTER SET = latin1;


-- -----------------------------------------------------
-- Table `aston`.`t_value_type`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `aston`.`t_value_type` (
  `pk_value_type` INT NOT NULL,
  `description` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`pk_value_type`),
  UNIQUE INDEX `description_UNIQUE` (`description` ASC) VISIBLE)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `aston`.`t_purchases`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `aston`.`t_purchases` (
  `pk_invoice_in` INT NOT NULL,
  `fk_supplier_id` INT NOT NULL,
  `value` FLOAT NOT NULL,
  `description` VARCHAR(100) NULL DEFAULT NULL,
  `vat` FLOAT NULL DEFAULT NULL,
  `fk_value_type` INT NOT NULL,
  PRIMARY KEY (`pk_invoice_in`),
  INDEX `fk_value_type_idx` (`fk_value_type` ASC) VISIBLE,
  CONSTRAINT `fk_value_type`
    FOREIGN KEY (`fk_value_type`)
    REFERENCES `aston`.`t_value_type` (`pk_value_type`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `aston`.`t_sales`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `aston`.`t_sales` (
  `pk_invoice_out` INT NOT NULL AUTO_INCREMENT,
  `fk_customer_id` INT NULL DEFAULT NULL,
  `fk_vat_type` INT NULL DEFAULT NULL,
  `vat_amount` FLOAT NULL DEFAULT NULL,
  `fk_sales_type` INT NULL DEFAULT NULL,
  `sales_amount` FLOAT NULL DEFAULT NULL,
  `sales_description` LONGTEXT NULL DEFAULT NULL,
  PRIMARY KEY (`pk_invoice_out`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `aston`.`t_sales_category`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `aston`.`t_sales_category` (
  `pk_sales` INT NOT NULL AUTO_INCREMENT,
  `sales_description` LONGTEXT NULL DEFAULT NULL,
  PRIMARY KEY (`pk_sales`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `aston`.`t_vat`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `aston`.`t_vat` (
  `pk_vat` INT NOT NULL AUTO_INCREMENT,
  `value` INT NOT NULL,
  `description` VARCHAR(45) NULL DEFAULT NULL,
  PRIMARY KEY (`pk_vat`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
```