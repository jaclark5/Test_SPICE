# SPICE Geometry Detection Testing

This repository contains notebooks and data for testing TMOS geometry filtering on the SPICE dataset, specifically identifying and characterizing suspicious structures.

## Directory Structure

### `Filter_SPICE_Suspicious/`

Filtering and flagging of suspicious SPICE records based on geometry criteria.

| File | Description |
|------|-------------|
| `test_smiles_spice_tmos_geometry_filter.ipynb` | Notebook implementing the geometry-based filter for suspicious SPICE structures |
| `spice_upload_fails_atoms_too_close.json` | Records flagged for the **"Atoms too close"** criterion (see below) |
| `flagged_df_smiles.csv` / `.txt` | SMILES for all flagged records |
| `skip_records_smiles.csv` / `.txt` | SMILES for records to be skipped/excluded |

#### "Atoms too close" criterion (`spice_*atoms_too_close.json`)

Structures were flagged if:
- Two **bonded** atoms were closer than **0.7×** the sum of their covalent radii, or
- Two **non-bonded** atoms were closer than **1.0×** the sum of their covalent radii.

These represent the most egregious geometry issues in the dataset. Two categories of problems were found:

- **PubChem subsets:** Typically "squished" phosphate and sulfate groups — known problems for Sage 2.0.
- **Amino Acid Ligand subset:** Cases where atoms appear to have been permuted by accident, resulting in a broken topology. It is unclear whether the underlying QM calculation is valid (with only the topology record being wrong) or whether the entire entry is corrupted.

---

### `Test_TMOS_SMILES/`

Testing TMOS SMILES assignment and bond order determination on SPICE structures.

| File | Description |
|------|-------------|
| `test_smiles_spice_tmos.ipynb` | Main notebook for TMOS SMILES testing |
| `view_bond_order_mismatches.ipynb` | Notebook for inspecting bond order mismatches |
| `output_errored.json` | Records that errored during TMOS processing |
| `output_no_excuse.json` | Records that failed without an identifiable cause |
| `output_xyz.json` | XYZ geometry output for processed records |
