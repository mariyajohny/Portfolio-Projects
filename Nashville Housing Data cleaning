
--Cleaning Data in SQL Queries



Select *
From [dbo].[NashVille Housing]
--------------------------------------------------------------------------------------------------------------------------

-- Standardize Date Format

Select SaleDateConverted, CONVERT(Date,SaleDate)
From [dbo].[NashVille Housing]

Update [NashVille Housing]
Set SaleDate = Convert(Date,SaleDate)

ALTER TABLE [NashVille Housing]
Add SaleDateConverted Date;

Update [NashVille Housing]
SET SaleDateConverted = CONVERT(Date,SaleDate)

-- Populate Property Address data

Select *
From [dbo].[NashVille Housing]
--Where PropertyAddress is null
order by ParcelID

Select a.ParcelID, a.PropertyAddress, b.ParcelID, b.PropertyAddress, ISNULL(a.propertyaddress,b.PropertyAddress)
From [dbo].[NashVille Housing] a
JOIN [dbo].[NashVille Housing] b
	on a.ParcelID = b.ParcelID
	And a.[UniqueID ] <> b.[UniqueID ]
Where a.PropertyAddress is null

Update a
SET PropertyAddress = ISNULL(a.propertyaddress,b.PropertyAddress)
From [dbo].[NashVille Housing] a
JOIN [dbo].[NashVille Housing] b
	on a.ParcelID = b.ParcelID
	And a.[UniqueID ] <> b.[UniqueID ]
Where a.PropertyAddress is null

-- Breaking out Address into Individual Columns (Address, City, State)


Select PropertyAddress
From [dbo].[NashVille Housing]
--Where PropertyAddress is null
--order by ParcelID

SELECT
SUBSTRING(PropertyAddress, 1, CHARINDEX(',', PropertyAddress) -1 ) as Address
, SUBSTRING(PropertyAddress, CHARINDEX(',', PropertyAddress) + 1 , LEN(PropertyAddress)) as Address

From [dbo].[NashVille Housing]


ALTER TABLe [dbo].[NashVille Housing]
Add PropertySplitAddress Nvarchar(255);

Update [dbo].[NashVille Housing]
SET PropertySplitAddress = SUBSTRING(PropertyAddress, 1, CHARINDEX(',', PropertyAddress) -1 )


ALTER TABLE [dbo].[NashVille Housing]
Add PropertySplitCity Nvarchar(255);

Update [dbo].[NashVille Housing]
SET PropertySplitCity = SUBSTRING(PropertyAddress, CHARINDEX(',', PropertyAddress) + 1 , LEN(PropertyAddress))

Select *
From [dbo].[NashVille Housing]






Select OwnerAddress
From [dbo].[NashVille Housing]


Select
PARSENAME(Replace(OwnerAddress,',','.'), 3)
,PARSENAME(Replace(OwnerAddress,',','.'), 2)
,PARSENAME(Replace(OwnerAddress,',','.'), 1)
From [dbo].[NashVille Housing]




ALTER TABLe [dbo].[NashVille Housing]
Add OwnerSplitAddress Nvarchar(255);

Update [dbo].[NashVille Housing]
SET OwnerSplitAddress = PARSENAME(Replace(OwnerAddress,',','.'), 3)


ALTER TABLE [dbo].[NashVille Housing]
Add OwnerSplitCity Nvarchar(255);

Update [dbo].[NashVille Housing]
SET OwnerSplitCity = PARSENAME(Replace(OwnerAddress,',','.'), 2)

ALTER TABLE [dbo].[NashVille Housing]
Add OwnerSplitState Nvarchar(255);

Update [dbo].[NashVille Housing]
SET OwnerSplitState = PARSENAME(Replace(OwnerAddress,',','.'), 1)

Select *
From [dbo].[NashVille Housing]







--------------------------------------------------------------------------------------------------------------------------


-- Change Y and N to Yes and No in "Sold as Vacant" field


Select Distinct(SoldAsVacant), Count(SoldAsVacant)
From [dbo].[NashVille Housing]
Group by SoldAsVacant
order by 2


Select SoldAsVacant
, CASE When SoldAsVacant = 'Y' THEN 'Yes'
	   When SoldAsVacant = 'N' THEN 'No'
	   ELSE SoldAsVacant
	   END
From [dbo].[NashVille Housing]

Update [dbo].[NashVille Housing]
SET SoldAsVacant = CASE When SoldAsVacant = 'Y' THEN 'Yes'
	   When SoldAsVacant = 'N' THEN 'No'
	   ELSE SoldAsVacant
	   END


-----------------------------------------------------------------------------------------------------------------------------------------------------------

-- Remove Duplicates

WITH RowNumCTE AS(
Select *,
	ROW_NUMBER() OVER (
	PARTITION BY ParcelID,
				 PropertyAddress,
				 SalePrice,
				 SaleDate,
				 LegalReference
				 ORDER BY
					UniqueID
					) row_num

From [dbo].[NashVille Housing]
--order by ParcelID
)
select*
From RowNumCTE
Where row_num > 1
Order by PropertyAddress

Select *
From 


---------------------------------------------------------------------------------------------------------

-- Delete Unused Columns



Select *
From [dbo].[NashVille Housing]


ALTER TABLE [dbo].[NashVille Housing]
DROP COLUMN OwnerAddress, TaxDistrict, PropertyAddress, SaleDate
