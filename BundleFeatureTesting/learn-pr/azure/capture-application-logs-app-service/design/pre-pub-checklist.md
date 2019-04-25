---
ms.openlocfilehash: 160c1b58e136a514c6a957621ed13b556853cbe0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
---
# <a name="pre-publication-checklist"></a>Pre-publication checklist
1. Metadata
1. Content/Media/assets
1. Index.yml
1. All other yml files
1. Exercises
  
## <a name="metadata"></a>Metadata
- [X] is the uid set in all yml files?

### <a name="contentmediaassets"></a>Content/Media/assets
- [X] Remove regions from urls
- [ ] Final images/screenshots are present
- [X] Badge images are present
- [ ] Verify Acrolinx score for all content (score > 80)

### <a name="indexyml"></a>Index.yml
- [X] *title* is set
- [X] *description* is set and follows guidelines (doesn't duplicate title)
- [X] *summary* is set and follows guidelines
- [X] *abstract* is set and lists objectives (no periods)
- [X] *prerequisites* are set
- [ ] *ms.date* is set to publication date
- [X] *author* and *ms.author* are set
- [X] *ms.prod* is set to **learning-azure**
- [X] *iconUrl* is set and points to a valid svg
- [X] *badge* has *uid* child set to uid
- [X] all units are listed

### <a name="all-other-yml-files"></a>All other yml files
- [X] *uid* is set and matches index.yml
- [X] *title* is set
- [X] *ms.date* is set 
- [X] *author* and *ms.author* are set
- [ ] *durationInMinutes* is set and IS ACCURATE
- [X] *interactive* is set to **bash** or **azure-portal** (if exercise)
- [X] *azureSandbox* is set to true if needed
- [ ]  Knowledge checks reviewed for spelling and accuracy
- [X] *ROBOTS: NOINDEX*

### <a name="exercises"></a>Exercises
- [ ] Sandbox permissions have been requested 
- [X] All exercise units have *Exercise - * prefix on titles
- [ ] Used dynamic resource group name (where appropriate)
- [X] Sample or starter code is in public repo
- [ ] Task validation has been tested (if used)
- [ ] Exercises have been tested in their published environment (sandbox, VM, etc.)
