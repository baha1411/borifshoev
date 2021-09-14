# Sql
## Запрос ProductType:
```sql
USE [borifshoev]
GO

INSERT INTO [dbo].[ProductType]
           ([Title])

SELECT DISTINCT[Тип продукции]
  FROM [dbo].[products_k_import$]
   
```

## Запрос MaterialType:
```sql
USE [borifshoev]
GO

INSERT INTO [dbo].[MaterialType]
           ([Title])

		   
SELECT DISTINCT[Типматериала]
  FROM [dbo].[Лист1$]
   
```

## Запрос Material:
```sql
USE [borifshoev]
GO

INSERT INTO [dbo].[Material]
           ([Title]
           ,[CountInPack]
           ,[Unit]
           ,[CountInStock]
           ,[MinCount]
           ,[Cost]
           ,[MaterialTypeID])

SELECT [Наименованиематериала]
      ,[Количествовупаковке]
      ,[Единицаизмерения]
      ,[Количествонаскладе]
      ,[Минимальныйвозможныйостаток]
      ,[Стоимость]
	  ,MT.ID
  FROM [dbo].[Лист1$] l,

  MaterialType MT

  Where MT.Title=l.Типматериала
   
```

## Запрос Product:
```sql
USE [borifshoev]
GO

INSERT INTO [dbo].[Product]
           ([Title]
           ,[ProductTypeID]
           ,[ArticleNumber]
           ,[Image]
           ,[ProductionPersonCount]
           ,[ProductionWorkshopNumber]
           ,[MinCostForAgent])

SELECT [Наименование продукции]
	  ,PT.ID
      ,[Артикул]
      ,[Изображение]
      ,[Количество человек для производства]
      ,[Номер цеха для производства]
      ,[Минимальная стоимость для агента]
  FROM [dbo].[products_k_import$] PAI,

  ProductType PT

  Where PT.Title=PAI.[Тип продукции]
   
```

## Запрос ProductMaterial:
```sql
USE [borifshoev]
GO

INSERT INTO [dbo].[ProductMaterial]
           ([ProductID]
           ,[MaterialID]
           ,[Count])


SELECT P.ID
      ,M.ID
      ,[Необходимое количество материала]
  FROM [dbo].[ProductMaterial_Import$] PM,

  Material M,
  Product P

  Where P.Title=PM.Продукция AND M.Title=PM.[Наименование материала]
### UseCase
![UseCase](/UseCase.png) 
