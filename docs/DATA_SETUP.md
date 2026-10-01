# Data setup

This repository does not redistribute BUSI or BrEaST-Lesions-USG images.

## BUSI

Obtain the dataset from the original source and configure the repository as:

data/Dataset_BUSI_with_GT/{benign,malignant,normal}

The binary experiments use benign and malignant images. Normal images are retained for audit purposes but excluded from classification.

## BrEaST-Lesions-USG

Obtain the dataset and metadata from its original source. Configure the local dataset path in Pass 6A and place the metadata workbook under data/metadata/.

Do not commit patient/image data or restricted metadata to this repository.
