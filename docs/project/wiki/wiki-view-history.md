---
title: Revert changes and find wiki page history
titleSuffix: Azure DevOps
description: Add and update pages offline for your built-in team project wiki 
ms.technology: devops-collab
ms.custom: wiki, devdivchpfy22
ms.topic: how-to
ms.author: chcomley
author: chcomley
ms.reviewer: gopinach
monikerRange: '<= azure-devops'
ms.date: 06/13/2022  
---

# View wiki page history and revert changes

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]  

You can see details of the changes made to a wiki page and revert to an earlier version, if needed.

<a id="view-revision-history"></a>

## View wiki page revision history  

1. To view the revision history of a page, select the **Revisions** link provided on each page. You can also select **View revisions** in the context menu of a page.

   :::image type="content" source="media/wiki/click-revision.png" alt-text="Screenshot of the context menu showing Print, Link work items, View revisions, and Delete options. View revisions is highlighted.":::

2. Revision pages show who made the change along with the revision message, date, and version or commit ID. To view details of a revision, select the message or version link.

	::: moniker range=">= azure-devops-2019"

   > [!div class="mx-imgBorder"]  
   > ![Page for a provisioned wiki page](media/wiki/revision-history-vsts.png)

   ::: moniker-end

   ::: moniker range="tfs-2018"

   ![Home | Revisions lists revisions. The columns are Author, Message, Last Updated, and Version.](media/wiki/revision-history.png) 

   ::: moniker-end

3. Similar to any git file revision, the revision details page provides a **Show diff side-by-side** view or the **Show diff inline** view. Choose **Preview** to see the content of the page of the specific revision.

   ![Two revisions of an article are compared side-by-side. The article is in Markdown, and is titled Welcome to the Fabrikam Fiber wiki.](media/wiki/wiki-revision-details-2.png)  

   ::: moniker range=">= azure-devops-2019"

   For a *publish as code wiki* page, you see similar information, but **Revert** isn't active.

   > [!div class="mx-imgBorder"]  
   > ![Revision page for a publish as code wiki page](media/wiki/view-history-publish-as-code.png)

   ::: moniker-end

4. [Use the breadcrumbs](../navigation/use-breadcrumbs-selectors.md) to return to the page or revisions of the page.


<a id="revert-provision"></a>

## Revert a commit to a *provisioned wiki* page

Select **Revert** on the revision details page to revert a change on a wiki page.

::: moniker range="tfs-2018"
> [!NOTE]
> The **Revert** option is available with TFS 2018.2 and later versions.
::: moniker-end

![Dialog box Revert revision 701b5a9f has the Revert and Cancel options. Revert is selected.](media/wiki/wiki-revert.png) 

<a id="revert-publish"></a>

::: moniker range=">= azure-devops-2019"

## Revert a commit to a *publish as code wiki* page

If you need to revert to an earlier revision for a page that you've published as code, do one of the following actions:

- If the commit is the most recent revision to a page, you can revert from the web portal.
- If the commit is an earlier revision, with additional commits having occurred in between, create a separate branch and revert the changes in that branch.

### Revert from a recent revision from the web portal

1. Preview any version by choosing the commit ID from the **Revisions** page for the selected file.

2. Copy the full ID of the commit by selecting :::image type="icon" source="../../media/icons/copy-clone-icon.png" border="false"::: **Copy-clone**.  Here we copy the commit ID, `ca6d475a22eb1db930cf238f3b80862a78a689e4`, with the abbreviated ID of `ca6d475a`.

	> [!div class="mx-imgBorder"]  
	> ![Copy the full commit id for an earlier commit](media/wiki/revert-publish-as-code-copy-commit-id.png)

3. Open the **Repos > Commits** page and paste the ID that you copied into the Commit ID box and choose :::image type="icon" source="../../media/icons/search-icon.png" border="false"::: Search.
 
	> [!div class="mx-imgBorder"]  
	> ![Paste the commit id for an earlier commit.](media/wiki/revert-publish-as-code-paste-commit-id.png)
	
4. From the commit page, select :::image type="icon" source="../../media/icons/actions-icon.png" border="false"::: **More actions**, and then choose **Revert**.  

	> [!div class="mx-imgBorder"]  
	> ![Choose revert menu option of an earlier commit](media/wiki/revert-publish-as-code-option.png)

5. Confirm that you want to revert. Choose **Revert** in the dialog.  

	> [!div class="mx-imgBorder"]  
	> ![Revert commit dialog](media/wiki/revert-publish-as-code-commit-dialog.png)

	A branch is created with the reverted changes.

6. Select **Create Pull Request**.  

	> [!div class="mx-imgBorder"]  
	> ![Select Create Pull Request.](media/wiki/revert-publish-as-code-commit-confirm.png)
		
	If instead, you receive an error message as shown, it indicates that you must create a local branch and make your changes manually as described in the next section.

	> [!div class="mx-imgBorder"]  
	> ![Revert publish code as wiki error message](media/wiki/revert-publish-as-code-error-message.png)

7. Select **Create** in the New Pull Request form.

8. Select **Complete** to merge the changes into the main wiki branch. Optionally, check the **Delete** checkbox to delete the intermediate branch.

	> [!div class="mx-imgBorder"]  
	> ![Revert publish code as wiki, complete pull request](media/wiki/revert-complete-pull-request-dialog.png)

Return to the wiki, refresh the browser, and you should see the reverted content.

### Revert from earlier revisions using a different branch

To revert to an earlier committed version of a publish as code wiki page (one that isn't the immediate last revision), you must update a branch other than the main branch for the wiki, and then create a pull request to the main branch.

1. Create a local branch of the main wiki branch.
1. View the commit history and locate the commit that contains the changes you want to undo.
2. Use the revert command to revert the desired commit.
3. When a conflict arises, use the conflict resolution tools to resolve the issues.
4. Commit the changes locally to your local branch.
5. Push the local branch to the remote server.
6. Create a pull request for your local branch into main.
7. Complete the pull request.

You can use the following steps to identify the commit that contains the content you want to revert to. Then, use standard Git operations to revert the content.

For more information, see the following articles:

- [Clone an existing Git repo](../../repos/git/clone.md)  
- [Create work in branches](../../repos/git/create-branch.md)  
- [Review history](../../repos/git/review-history.md)  
- [Undo (revert) changes](../../repos/git/undo.md)
- [Resolve merge conflicts](../../repos/git/merging.md)
- [Copy changes with cherry-pick](../../repos/git/cherry-pick.md)
- [Commit details](../../repos/git/commit-details.md)

::: moniker-end

## Related articles

- [Wiki Git repository files and file structure](wiki-file-structure.md)
- [Differences between provisioned wiki and publish code as wiki](provisioned-vs-published-wiki.md)
- [Update wiki pages offline](wiki-update-offline.md)
- [Manage README and Wiki permissions](manage-readme-wiki-permissions.md)