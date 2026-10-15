# How-To: Add Fields to the Opportunity List View Mass Update

**Story:** [#137 Add Closed Lost Fields to List View Mass Update](https://trello.com/c/2hNKLaAa/137-add-closed-lost-fields-to-list-view-mass-update)
**Date:** 2026-10-15
**Audience:** Chris (implementation), Sarah (future self-service)

## Background

The "mass update" is Salesforce's standard **list view inline edit**. You can only edit a field across many records at once if that field is a **column** in the list view. The first round (2026-09-21, prod) added Lost Category, Lost Reason and Lost Reason Notes.

The mass Closed Lost failed because **Lost Detail** and **Timeline to Evaluate New Software** are required when Stage = Closed Lost, and neither was in the view. Salesforce saves all of the edits on a row in one go, so every required field has to be fillable from the view. Sarah also asked for **Opportunity Source**, which has nothing to do with Closed Lost.

## Change for this update (prod)

On the same Opportunity list view, add these columns:

1. Opportunity Source
2. Lost Detail
3. Timeline to Evaluate New Software

This is a list view setting, not metadata, so no change set is needed. Make the change in prod in the list view the team already uses.

Check afterwards: pick 2–3 test Opportunities and set Stage = Closed Lost plus all five Lost fields (Category, Reason, Reason Notes, Detail, Timeline) in a single save. The save should go through with no validation error.

---

## How-To for Sarah: adding a field to the mass update yourself

### Add a column to the list view

1. Go to **Opportunities** and open the list view you use for mass updates.
2. Click the **gear icon** (List View Controls) to the right of the search box.
3. Choose **Select Fields to Display**.
4. Find the field under **Available Fields** and click the **right arrow** to move it to **Visible Fields**. Use the up/down arrows to set the order.
5. Click **Save**.

> **Gear options greyed out?** The view is shared and you don't have permission to edit it. Use **Gear → Clone** to make your own copy, then add the columns there. Or ask Chris to add them to the shared view.

### Mass-update records

1. Tick the checkboxes for the records you want to change (up to 200 at a time).
2. On one of the selected rows, click the **pencil** in the cell you want to change.
3. Enter the value, tick **"Update N selected items"**, and click **Apply**.
4. Repeat for each field. **For Closed Lost, fill in every required Lost field** (Lost Category, Lost Reason, Lost Reason Notes, Lost Detail, Timeline to Evaluate New Software) **before** you click Save, together with Stage.
5. Click **Save** at the bottom of the list.

### If it fails

- **A row errors with "required" or a validation message:** a required field isn't in the view, or was left blank. Add the column (see above), fill it in, and save again.
- **No pencil on a field:** the field is read-only for your profile, is a formula field, or the list view shows more than one record type. Filter the view down to a single Opportunity record type and try again. If it's still locked, ask Chris.
- **Lost Reason won't take a value:** it may depend on Lost Category. Set Lost Category first, click Apply, then set Lost Reason.
