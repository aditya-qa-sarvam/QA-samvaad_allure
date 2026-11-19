# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: deploy\bugreplicator.spec.ts >> Bug Replicator >> A Paused campaign must not resume while its phone numbers are Archived
- Location: tests\deploy\bugreplicator.spec.ts:156:7

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByRole('button', { name: 'Archived', exact: true })
Expected: visible
Timeout: 15000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" with timeout 15000ms
  - waiting for getByRole('button', { name: 'Archived', exact: true })

```

```yaml
- region "Notifications alt+T"
- complementary:
  - heading "Voice Agents" [level=2]
  - text: Free plan
  - button
  - button "Search":
    - paragraph: Search
    - text: Ctrl+K
  - link "Home":
    - /url: /samvaad/home
    - paragraph: Home
  - paragraph: Build
  - link "Agents":
    - /url: /samvaad/build/my-agents
    - paragraph: Agents
  - link "Workflows":
    - /url: /samvaad/build/workflows
    - paragraph: Workflows
  - link "Knowledge base":
    - /url: /samvaad/build/knowledge-base
    - paragraph: Knowledge base
  - link "Integrations":
    - /url: /samvaad/integrations
    - paragraph: Integrations
  - paragraph: Deploy
  - link "Phone numbers":
    - /url: /samvaad/deploy/phone-numbers/fc0af4b6-25-2fc2a5c1-d3d5
    - paragraph: Phone numbers
  - link "Inbound calls":
    - /url: /samvaad/deploy/inbounds
    - paragraph: Inbound calls
  - link "Outbound campaigns":
    - /url: /samvaad/deploy/campaigns
    - paragraph: Outbound campaigns
  - link "Experiments Beta":
    - /url: /samvaad/deploy/experiments
    - paragraph: Experiments
    - text: Beta
  - link "Deploy with code":
    - /url: /samvaad/deploy/with-code
    - paragraph: Deploy with code
  - paragraph: Monitor
  - link "Agent analytics":
    - /url: /samvaad/monitor/agent-analytics
    - paragraph: Agent analytics
  - link "Workflow Analytics":
    - /url: /samvaad/monitor/workflow-analytics
    - paragraph: Workflow Analytics
  - link "Connect New":
    - /url: /samvaad/monitor/connect
    - paragraph: Connect
    - text: New
  - link "Boards":
    - /url: /samvaad/monitor/boards
    - paragraph: Boards
  - link "Call logs":
    - /url: /samvaad/monitor/agent-analytics/call-logs
    - paragraph: Call logs
  - paragraph: More
  - link "Settings":
    - /url: /samvaad/settings/api-key
    - paragraph: Settings
  - link "MCP New":
    - /url: /samvaad/mcp
    - paragraph: MCP
    - text: New
  - link "Usage":
    - /url: /samvaad/usage
    - paragraph: Usage
  - link "Pricing":
    - /url: /samvaad/pricing
    - paragraph: Pricing
  - link "Documentation":
    - /url: https://docs.sarvam.ai/conversations/overview
    - paragraph: Documentation
  - button "What's new New":
    - paragraph: What's new
    - text: New
  - button "RA Ram Goel":
    - text: RA
    - paragraph: Ram Goel
- main:
  - heading "Phone Numbers" [level=4]
  - text: /
  - button "Sarvam Vobiz":
    - heading "Sarvam Vobiz" [level=4]
  - button "Ask Genie":
    - paragraph: Ask Genie
  - button "Add connection":
    - paragraph: Add connection
  - button "View details":
    - paragraph: View details
  - paragraph: Total
  - heading "12" [level=1]
  - paragraph: Active
  - heading "7" [level=1]
  - paragraph: Archived
  - heading "5" [level=1]
  - paragraph: Released
  - heading "0" [level=1]
  - tablist:
    - tab "All numbers" [selected]:
      - paragraph: All numbers
    - tab "Unassigned":
      - paragraph: Unassigned
    - tab "Archived":
      - paragraph: Archived
    - tab "Released":
      - paragraph: Released
  - button "All groups"
  - button "Buy number":
    - paragraph: Buy number
  - textbox "Search by number": "+917965853872"
  - table:
    - rowgroup:
      - row "Number Group Status Added Updated Renews At":
        - columnheader:
          - paragraph
        - columnheader "Number":
          - paragraph: Number
        - columnheader "Group":
          - paragraph: Group
        - columnheader "Status":
          - paragraph: Status
        - columnheader "Added":
          - paragraph: Added
        - columnheader "Updated":
          - paragraph: Updated
        - columnheader "Renews At":
          - paragraph: Renews At
        - columnheader:
          - paragraph
    - rowgroup:
      - row "+917965853872 — Archived 10 Sept 2026, 01:53 am 19 Nov 2026, 01:16 pm 8 Dec 2026, 11:53 pm":
        - cell:
          - checkbox
        - cell "+917965853872":
          - paragraph: "+917965853872"
        - cell "—":
          - paragraph: —
        - cell "Archived"
        - cell "10 Sept 2026, 01:53 am":
          - paragraph: 10 Sept 2026, 01:53 am
        - cell "19 Nov 2026, 01:16 pm":
          - paragraph: 19 Nov 2026, 01:16 pm
        - cell "8 Dec 2026, 11:53 pm":
          - paragraph: 8 Dec 2026, 11:53 pm
        - cell:
          - button
- alert: Indus by Sarvam
```

# Test source

```ts
  1694 |       console.log("[Archive] Actually archived numbers:", archivedNumbers);
  1695 | 
  1696 |       return {
  1697 |         status: "archived",
  1698 |         archivedNumbers,
  1699 |       };
  1700 |     }
  1701 | 
  1702 |     // =====================================================
  1703 |     // CASE 2 - NORMAL ARCHIVE
  1704 |     //
  1705 |     // All selected numbers can be archived.
  1706 |     // =====================================================
  1707 | 
  1708 |     if (state === "archive-dialog") {
  1709 |       const archiveDialog = this.page.getByRole("dialog").filter({
  1710 |         has: archiveDialogHeading,
  1711 |       });
  1712 | 
  1713 |       await expect(archiveDialog).toBeVisible({
  1714 |         timeout: 10000,
  1715 |       });
  1716 | 
  1717 |       const confirmArchiveButton = archiveDialog.getByRole("button", {
  1718 |         name: "Archive",
  1719 |         exact: true,
  1720 |       });
  1721 | 
  1722 |       await expect(confirmArchiveButton).toBeVisible({
  1723 |         timeout: 10000,
  1724 |       });
  1725 | 
  1726 |       await expect(confirmArchiveButton).toBeEnabled();
  1727 | 
  1728 |       console.log("[Archive] All selected numbers are eligible.");
  1729 | 
  1730 |       await confirmArchiveButton.click();
  1731 | 
  1732 |       // ===================================================
  1733 |       // VERIFY SUCCESS TOAST
  1734 |       // ===================================================
  1735 | 
  1736 |       const successToast = this.page.getByText(/\d+\s+numbers?\s+archived/i);
  1737 | 
  1738 |       await expect(successToast).toBeVisible({
  1739 |         timeout: 15000,
  1740 |       });
  1741 | 
  1742 |       const successMessage = (await successToast.textContent())?.trim();
  1743 | 
  1744 |       console.log(`[Archive] SUCCESS: ${successMessage}`);
  1745 | 
  1746 |       return {
  1747 |         status: "archived",
  1748 |         archivedNumbers: selectedNumbers,
  1749 |       };
  1750 |     }
  1751 | 
  1752 |     // =====================================================
  1753 |     // CASE 3 - ALL SELECTED NUMBERS ARE BLOCKED
  1754 |     //
  1755 |     // Toast means archive cannot be performed.
  1756 |     // =====================================================
  1757 | 
  1758 |     if (state === "blocked-toast") {
  1759 |       const toastMessage = (
  1760 |         await blockedToastMessage.first().textContent()
  1761 |       )?.trim();
  1762 | 
  1763 |       console.log(`[Archive] BLOCKED: ${toastMessage}`);
  1764 | 
  1765 |       console.log(
  1766 |         "[Archive] Archive cannot be performed because selected numbers are associated with active deployments.",
  1767 |       );
  1768 | 
  1769 |       return {
  1770 |         status: "conflict",
  1771 |         archivedNumbers: [],
  1772 |       };
  1773 |     }
  1774 | 
  1775 |     // =====================================================
  1776 |     // UNKNOWN UI STATE
  1777 |     // =====================================================
  1778 | 
  1779 |     throw new Error(
  1780 |       "Archive flow failed: no expected archive dialog, conflict dialog, or blocking toast appeared.",
  1781 |     );
  1782 |   }
  1783 | 
  1784 |   // =========================================================
  1785 |   // OPEN ARCHIVED TAB
  1786 |   // =========================================================
  1787 | 
  1788 |   async openArchivedTab() {
  1789 |     const archivedTab = this.page.getByRole("button", {
  1790 |       name: "Archived",
  1791 |       exact: true,
  1792 |     });
  1793 | 
> 1794 |     await expect(archivedTab).toBeVisible();
       |                               ^ Error: expect(locator).toBeVisible() failed
  1795 | 
  1796 |     await archivedTab.click();
  1797 | 
  1798 |     console.log("Archived tab opened");
  1799 |   }
  1800 | 
  1801 |   // =========================================================
  1802 |   // SELECT SPECIFIC ARCHIVED NUMBERS
  1803 |   // =========================================================
  1804 | 
  1805 |   async selectArchivedNumbers(phoneNumbers: string[]): Promise<void> {
  1806 |     console.log(
  1807 |       `[Archived] Selecting ${phoneNumbers.length} archived number(s)...`,
  1808 |     );
  1809 | 
  1810 |     const dataTable = this.phoneNumbersTable();
  1811 | 
  1812 |     await expect(dataTable).toBeVisible({
  1813 |       timeout: 10000,
  1814 |     });
  1815 | 
  1816 |     for (const phoneNumber of phoneNumbers) {
  1817 |       const row = dataTable
  1818 |         .getByRole("row")
  1819 |         .filter({
  1820 |           has: dataTable.getByRole("cell", {
  1821 |             name: phoneNumber,
  1822 |             exact: true,
  1823 |           }),
  1824 |         })
  1825 |         .first();
  1826 | 
  1827 |       await expect(
  1828 |         row,
  1829 |         `Archived phone number ${phoneNumber} was not found`,
  1830 |       ).toBeVisible({
  1831 |         timeout: 10000,
  1832 |       });
  1833 | 
  1834 |       const numberCell = row.getByRole("cell", {
  1835 |         name: phoneNumber,
  1836 |         exact: true,
  1837 |       });
  1838 | 
  1839 |       await numberCell.click();
  1840 | 
  1841 |       console.log(`[Archived] Selected: ${phoneNumber}`);
  1842 |     }
  1843 | 
  1844 |     console.log(
  1845 |       `[Archived] SUCCESS: Selected ${phoneNumbers.length} archived number(s).`,
  1846 |     );
  1847 |   }
  1848 | 
  1849 |   // =========================================================
  1850 |   // VERIFY STATUS IS ARCHIVED
  1851 |   // =========================================================
  1852 | 
  1853 |   async verifyArchivedStatus(phoneNumbers: string[]) {
  1854 |     const searchBox = this.page.getByRole("textbox", {
  1855 |       name: "Search by number",
  1856 |     });
  1857 | 
  1858 |     await expect(searchBox).toBeVisible();
  1859 | 
  1860 |     for (const phoneNumber of phoneNumbers) {
  1861 |       await searchBox.fill(phoneNumber);
  1862 | 
  1863 |       const row = this.page.getByRole("row").filter({
  1864 |         hasText: phoneNumber,
  1865 |       });
  1866 | 
  1867 |       await expect(
  1868 |         row,
  1869 |         `Archived phone number ${phoneNumber} not found`,
  1870 |       ).toBeVisible();
  1871 | 
  1872 |       // Archived table:
  1873 |       // 0 = checkbox
  1874 |       // 1 = Number
  1875 |       // 2 = Status
  1876 |       const statusCell = row.getByRole("cell").nth(2);
  1877 | 
  1878 |       await expect(statusCell, `${phoneNumber} is not Archived`).toContainText(
  1879 |         "Archived",
  1880 |       );
  1881 | 
  1882 |       console.log(`SUCCESS: ${phoneNumber} = Archived`);
  1883 | 
  1884 |       await searchBox.clear();
  1885 |     }
  1886 | 
  1887 |     console.log(`SUCCESS: Verified ${phoneNumbers.length} archived numbers`);
  1888 |   }
  1889 | 
  1890 |   // =========================================================
  1891 |   // RESTORE SELECTED NUMBERS
  1892 |   // =========================================================
  1893 | 
  1894 |   // async restoreSelectedNumbers() {
```