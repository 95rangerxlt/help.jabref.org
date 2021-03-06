---
title: Groups
helpCategories: ["Finding, sorting and cleaning entries"]
---

# Groups

Groups allow to structure a BibTeX database in a tree-like way that is similar to organizing files on disk in directories and subdirectories. The two main differences are:

-   While a file is always located in exactly one directory, an entry may be contained in more than one group.
-   Groups may use certain criteria to dynamically define their content. New entries that match these criteria are automatically contained in these groups. This feature is not available in common file systems, but in several Email clients (e.g. Thunderbird and Opera).

Selecting a group shows the entries contained in that group. Selecting multiple groups shows the entries contained in any group (union) or those contained in all groups (intersection), depending on the current settings. All this is explained in detail below.

Group definitions are database-specific; they are saved as a `@COMMENT` block in the `.bib`-file and are shared among all users. (Future versions of JabRef might support user-dependent groups.)

## Interface

The groups interface is shown in the side pane on the left of the screen. It can be toggled on or off by pressing <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>G</kbd> or by the groups button in the toolbar. The interface has several buttons, but most functions are accessed via a context ("right-click") menu. Drag and Drop is also supported.

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><h2 id="some-quick-examples">Some quick examples</h2>
<p>You might want to...</p>
<h3 id="just-create-a-group-and-assign-some-entries-to-it">...just create a group and assign some entries to it</h3>
<p>Ensure that the groups interface is visible. Press the <strong>New Group</strong> button, enter a name for the group, then press OK, leaving all values at their defaults. Now select the entries to be assigned to the group and use Drag and Drop to the group, or the option <strong>Add to group</strong> in the context menu. Finally select the group to see its content (which should be the entries you just assigned).</p>
<h3 id="use-the-keywords-field-to-group-the-entries">...use the <code>keywords</code> field to group the entries</h3>
<p>Ensure that the groups interface is visible. Press the <strong>New Group</strong> button, enter a name for the group, and select the option to dynamically group entries by searching a field for a keyword. Enter the keyword to search for, then click OK. Finally select the group to see its content (which should be all entries whose <code>keywords</code> field contains the keyword you specified).</p>
<h3 id="use-a-free-form-search-expression-to-define-a-group">...use a free-form search expression to define a group</h3>
<p>Ensure that the groups interface is visible. Press the <strong>New Group</strong> button, enter a name for the group, and select the option to dynamically group entries by a free-form search expression. Enter <code>author=smith</code> as a search expression (replace <code>smith</code> with a name that actually occurs in your database) and click <strong>OK</strong>. Finally select the group to see its content (which should be all entries whose <code>author</code> field contains the name you specified).</p>
<h3 id="combine-multiple-groups">...combine multiple groups</h3>
<p>Create two different groups (e.g. as described above). Click the <strong>Settings</strong> button and make sure that <strong>Union</strong> is selected. Now select both groups. You should see all entries contained in any of the two groups. Click <strong>Settings</strong> again and select <strong>Intersection</strong>. Now you should see only those entries contained in both groups (which might be none at all, or exactly the same entries as before in case both groups contain the same entries).</p>
<h3 id="identify-overlapping-groups">...identify overlapping groups</h3>
<p>JabRef allows you to easily identify groups that overlap with the currently selected groups (i.e. that contain at least one entry that is also contained in the currently selected groups). Click <strong>Settings</strong> and activate the option to highlight overlapping groups. Then select a group that overlaps with other groups. The other groups should be highlighted.</p></td>
</tr>
</tbody>
</table>

## Types of groups

In JabRef there are four different types of groups:

1.  The group **All Entries**, which -- as the name suggests -- contains all entries, is always present and cannot be edited or removed.
2.  **Static groups** behave like directories on disk and contain only those entries that you explicitly assign to them.
3.  **Dynamic groups based on keyword search** contain entries in which a certain BibTeX field (e.g. `keywords`) contains a certain keyword (e.g. `electrical`). This method does not require manual assignment of entries, but uses information that is already present in the database. If all entries in your database have suitable keywords in their `keywords` field, using this type of group might be the best choice.
4.  **Dynamic groups based on free-form search expressions** contain entries that match a specified search expression, using the same syntax as the [search panel](Search) on the side pane. This [syntax](Search#advanced) supports logical operators (`AND`, `OR`, `NOT`) and allows to specify one or more BibTeX fields to search, facilitating more flexible group definitions than a keyword search (e.g. `author=smith         and title=electrical`).

Every group that you create is of one of the last three types. The group editing dialog, which is invoked by double-clicking on a group, shows a short description of the selected/edited group in plain English.

## Groups structure, creating and removing groups

Just like directories, groups are structured like a tree, with the group **All Entries** at the root. By right-clicking on a group you can add a new group to the tree, either at the same level as the selected group or as a subgroup of it. The **New Group** button lets you create a new subgroup of the group **All Entries**, regardless of the currently selected group(s). The context menu also allows to remove groups and/or subgroups, to sort subgroups alphabetically, or to move groups to a different location in the tree. The latter can also be done by Drag and Drop, with the restriction that Drag and Drop does not support changing the order of a group's subgroups.

Undo and redo is supported for all edits.

### Static groups

Static groups are populated only by explicit manual assignment of entries. After creating a static group you select the entries to be assigned to it, and use either Drag and Drop or the main table's context menu to perform the assignment. To remove entries from a static group, select them and use the main table's context menu. There are no options to be configured.

This method of grouping requires that all entries have a unique BibTeX key. In case of missing or duplicate BibTeX keys, the assignment of the affected entries cannot be correctly restored in future sessions.

### Dynamic groups

The content of a dynamic group is defined by a logical condition. Only entries that meet this condition are contained in the group. This method uses the information stored in the database itself, and updates dynamically whenever the database changes.

Two types of conditions can be used:

**Searching a field for a keyword**  
This method groups entries in which a specified BibTeX field (e.g. `keywords`) contains a specified search term (e.g. `electrical`). Obviously, for this to work, the grouping field must be present in every entry, and its content must be accurate. The above example would group all entries referring to something electrical. Using the field `author` allows to group entries by a certain author, etc. The search can either be done as a plain-text or a regular expression search. In the former case, JabRef allows to manually assign/remove entries to/from the group by simply appending/removing the search term to/from the content of the grouping field. This makes sense only for the `keywords` field or for self-defined fields, but obviously not for fields like `author` or `year`.

**Using a free-form search expression**  
This is similar to the above, but rather than search a single field for a single search term, the [search expression syntax](Search#advanced) can be used, which supports logical operators (`AND`, `OR`, `NOT`) and allows to search multiple BibTeX fields. For example, the search expression `keywords=regression and not         keywords=linear` groups entries concerned with non-linear regression.

In the groups view, dynamic groups are shown in *italics* by default. This can be turned off in the preferences (Options → Preferences → Groups, box "Show dynamic groups in italics").

### Hierarchical context

By default, a group is **independent** of its position in the groups tree: When selected, only the group's contents are shown. However, especially when using dynamic groups, it is often useful to define a subgroup that **refines its supergroup**, i.e., when selected, entries contained in both groups are displayed. For example, create a supergroup containing entries with the keyword `distribution` and a subgroup containing entries with the keyword `gauss` that refines this supergroup. Selecting the subgroup now displays entries that match both conditions, i.e. are concerned with Gaussian distributions. By adding another refining subgroup for `laplace` to the original supergroup, the grouping can easily be extended. In the groups tree, refining groups have a special icon (this can be turned off in the preferences).

The logical complement to a refining group is a group that **includes its subgroups**, i.e. when selected, not only the group's own entries, but also its subgroups' entries are shown. In the groups tree, this type of group has a special icon (this can be turned off in the preferences).

## Viewing a group's entries, combining multiple groups

Selecting a group shows the entries contained in that group by highlighting them and, depending on the settings (accessible by clicking the **Settings** button), moving them to the top of the list and/or selecting them. These options are identical to those available for the regular search.

When multiple groups are selected, either the union or the intersection of their content is shown, depending on the current settings. This allows to quickly combine multiple conditions, e.g. if you have a static group `Extremely     Important` to which you assign all extremely important entries, you can view the extremely important entries in any other group by selecting both groups (this requires to have **Intersection** selected in the settings).

## Groups and searching

When viewing the contents of the selected group(s), a search can be performed within these contents using the regular search facility.

## Highlighting overlapping groups

The **Settings** button offers an option to highlight overlapping groups. If this is activated, upon selection of one or more groups, all groups that contain at least one of the entries contained in the currently selected group(s) are highlighted. This quickly identifies overlap between the groups' contents. You might, for example, create a group `To Read` that contains all entries which you plan to read. Now, whenever you select any group, the group `To Read` is highlighted if the selected group contains entries that you plan to read.

## New entries assigned to selected groups

The **Settings** button offers also an option to automatically assign new entries to selected groups. If this is activated, upon selection of one or more groups, all the new entries created will be assigned to the selected groups. This work both for entries created from menu button or entries pasted from clipboard. This option can also be enabled/disabled from the menu "option &gt; preferences &gt; group".

## Advanced features

After mastering the grouping concepts described above, the following advanced features might come in handy.

### Automatically creating dynamic groups

By clicking the **Automatically create groups for database** button, you can quickly create a set of groups appropriate for your database. This feature will gather all words found in a specific field of your choice, and create a group for each word. This is useful for instance if your database contains suitable keywords for all entries. By autogenerating groups based on the `keywords` field, you should have a basic set of groups at no cost.

You can also specify characters to ignore, for instance commas used between keywords. These will be treated as separators between words, and not part of them. This step is important for combined keywords such as `laplace     distribution` to be recognized as a single semantic unit. (You cannot use this option to remove complete words. Instead, delete the unwanted groups manually after they were created automatically.)

### Refreshing the groups view

The **Refresh** button updates the entry table to reflect the current groups selection. This is usually done automatically, but in rare occasions (e.g. after a group-related undo/redo) a manual refresh is required.

### Mixing refining groups with including groups

If a refining group is a subgroup of a group that includes its subgroups -- the refining group's siblings --, these siblings are ignored when the refining group is selected.
