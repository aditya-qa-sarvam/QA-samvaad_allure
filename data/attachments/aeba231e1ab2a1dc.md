# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: Build\datavalidator.spec.ts >> Agent - Data Validator >> Test 1 - Create Data Validator and verify it in Tools table
- Location: tests\Build\datavalidator.spec.ts:50:9

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByRole('dialog').getByRole('textbox', { name: 'Fixed value', exact: true })
Expected: visible
Timeout: 15000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" with timeout 15000ms
  - waiting for getByRole('dialog').getByRole('textbox', { name: 'Fixed value', exact: true })

```

```yaml
- region "Notifications alt+T"
- main
- dialog "Month Check969":
  - heading "Month Check969" [level=3]
  - paragraph: Check a value's format and validity, such as an email or phone number.
  - button "Close"
  - separator
  - text: "1"
  - heading "Name & describe the tool" [level=4]
  - text: Tool name *
  - textbox "Tool name *":
    - /placeholder: e.g. validate_dob
    - text: Month_check969
  - text: Use snake_case — e.g. validate_dob, check_phone. No spaces. What does this tool do? *
  - button "Improve":
    - paragraph: Improve
  - textbox "Creates a support ticket from a problem the caller reports.": Checks whether the caller's stated birthday month matches December. Call this only if the caller mentions their birthday or birth month during the conversation. If it matches, let the caller know they qualify for a 50 percent discount; if not, let them know pleasantly that the discount does not apply this time.
  - text: The agent uses the name and description of the tool to decide when to call it. 2
  - heading "What to validate" [level=4]
  - text: Input source
  - button "Fixed value"
  - text: Where the tool’s single subject value comes from. Fixed value *
  - textbox "Fixed value *":
    - /placeholder: e.g. 560001
  - text: Value type
  - button "String"
  - text: How the backend parses and checks the value (source of truth for type). Pattern (regex)
  - textbox "Pattern (regex)":
    - /placeholder: "e.g. ^[A-Z]{5}[0-9]{4}[A-Z]$"
  - text: Optional. Leave blank to only check that the value is a non-empty string. 3
  - heading "What the agent says" [level=4]
  - paragraph: Optional lines the agent can speak after the check. Leave blank to let the prompt decide.
  - text: On success
  - textbox "On success":
    - /placeholder: That looks good.
  - text: On fail
  - textbox "On fail":
    - /placeholder: That doesn’t look right. Could you try again?
  - text: On error
  - textbox "On error":
    - /placeholder: Something went wrong while checking that. Let’s try once more.
  - button "Advanced"
  - paragraph: Include in context
  - paragraph: Keep this tool available to the agent during the conversation.
  - switch "Include in context" [checked]
  - button "Cancel":
    - paragraph: Cancel
  - button "Add tool":
    - paragraph: Add tool
```

# Test source

```ts
  1108 |     await expect(fixedValueButton).toBeVisible();
  1109 | 
  1110 |     // -------------------------------------------------------
  1111 |     // Fixed value -> Agent variable
  1112 |     // -------------------------------------------------------
  1113 | 
  1114 |     await fixedValueButton.click();
  1115 | 
  1116 |     const agentVariableOption = this.page
  1117 |       .getByText("Agent variable", {
  1118 |         exact: true,
  1119 |       })
  1120 |       .last();
  1121 | 
  1122 |     await expect(agentVariableOption).toBeVisible();
  1123 | 
  1124 |     await agentVariableOption.click();
  1125 | 
  1126 |     await expect(
  1127 |       dialog.getByRole("button", {
  1128 |         name: "Agent variable",
  1129 |         exact: true,
  1130 |       }),
  1131 |     ).toBeVisible();
  1132 | 
  1133 |     console.log("Input source verified: Agent variable");
  1134 | 
  1135 |     // -------------------------------------------------------
  1136 |     // Agent variable -> Let the agent decide
  1137 |     // -------------------------------------------------------
  1138 | 
  1139 |     await dialog
  1140 |       .getByRole("button", {
  1141 |         name: "Agent variable",
  1142 |         exact: true,
  1143 |       })
  1144 |       .click();
  1145 | 
  1146 |     const agentDecideOption = this.page
  1147 |       .getByText("Let the agent decide", {
  1148 |         exact: true,
  1149 |       })
  1150 |       .last();
  1151 | 
  1152 |     await expect(agentDecideOption).toBeVisible();
  1153 | 
  1154 |     await agentDecideOption.click();
  1155 | 
  1156 |     await expect(
  1157 |       dialog.getByRole("button", {
  1158 |         name: "Let the agent decide",
  1159 |         exact: true,
  1160 |       }),
  1161 |     ).toBeVisible();
  1162 | 
  1163 |     console.log("Input source verified: Let the agent decide");
  1164 | 
  1165 |     // -------------------------------------------------------
  1166 |     // Let the agent decide -> Fixed value
  1167 |     // -------------------------------------------------------
  1168 | 
  1169 |     await dialog
  1170 |       .getByRole("button", {
  1171 |         name: "Let the agent decide",
  1172 |         exact: true,
  1173 |       })
  1174 |       .click();
  1175 | 
  1176 |     const fixedValueOption = this.page
  1177 |       .getByText("Fixed value", {
  1178 |         exact: true,
  1179 |       })
  1180 |       .last();
  1181 | 
  1182 |     await expect(fixedValueOption).toBeVisible();
  1183 | 
  1184 |     await fixedValueOption.click();
  1185 | 
  1186 |     await expect(
  1187 |       dialog.getByRole("button", {
  1188 |         name: "Fixed value",
  1189 |         exact: true,
  1190 |       }),
  1191 |     ).toBeVisible();
  1192 | 
  1193 |     console.log("Input source final state = Fixed value");
  1194 |   }
  1195 | 
  1196 |   // =========================================================
  1197 |   // ENTER FIXED VALUE
  1198 |   // =========================================================
  1199 | 
  1200 |   async fillDataValidatorFixedValue() {
  1201 |     const dialog = this.page.getByRole("dialog");
  1202 | 
  1203 |     const fixedValueInput = dialog.getByRole("textbox", {
  1204 |       name: "Fixed value",
  1205 |       exact: true,
  1206 |     });
  1207 | 
> 1208 |     await expect(fixedValueInput).toBeVisible({
       |                                   ^ Error: expect(locator).toBeVisible() failed
  1209 |       timeout: 15_000,
  1210 |     });
  1211 | 
  1212 |     await fixedValueInput.fill("December");
  1213 | 
  1214 |     await expect(fixedValueInput).toHaveValue("December");
  1215 | 
  1216 |     console.log("Fixed value = December");
  1217 |   }
  1218 | 
  1219 |   // =========================================================
  1220 |   // CHECK THE CALLER'S BIRTHDAY MONTH
  1221 |   // =========================================================
  1222 | 
  1223 |   /*
  1224 |    * Makes the validator actually check what the caller says.
  1225 |    *
  1226 |    * With a Fixed value and no Pattern, the validator only checks that the
  1227 |    * fixed text is non-empty, so it passes for every month. Instead:
  1228 |    *
  1229 |    *   Input source = Let the agent decide  (the agent passes the month
  1230 |    *                                          the caller said)
  1231 |    *   Pattern      = December, any letter case
  1232 |    *
  1233 |    * December -> "On success", any other month -> "On fail".
  1234 |    *
  1235 |    * The pattern spells out each letter's case instead of using an (?i)
  1236 |    * flag, so it means the same in every regex engine.
  1237 |    */
  1238 |   async setDataValidatorToCheckBirthdayMonth() {
  1239 |     const dialog = this.page.getByRole("dialog");
  1240 | 
  1241 |     // -------------------------------------------------------
  1242 |     // Fixed value -> Let the agent decide
  1243 |     // -------------------------------------------------------
  1244 | 
  1245 |     await dialog
  1246 |       .getByRole("button", {
  1247 |         name: "Fixed value",
  1248 |         exact: true,
  1249 |       })
  1250 |       .click();
  1251 | 
  1252 |     await this.page
  1253 |       .getByText("Let the agent decide", {
  1254 |         exact: true,
  1255 |       })
  1256 |       .last()
  1257 |       .click();
  1258 | 
  1259 |     await expect(
  1260 |       dialog.getByRole("button", {
  1261 |         name: "Let the agent decide",
  1262 |         exact: true,
  1263 |       }),
  1264 |     ).toBeVisible();
  1265 | 
  1266 |     // -------------------------------------------------------
  1267 |     // What the agent must pass in
  1268 |     // -------------------------------------------------------
  1269 | 
  1270 |     const inputParameter = dialog.getByRole("textbox", {
  1271 |       name: "Input parameter",
  1272 |     });
  1273 | 
  1274 |     await expect(inputParameter).toBeVisible({
  1275 |       timeout: 15_000,
  1276 |     });
  1277 | 
  1278 |     await inputParameter.fill(
  1279 |       "The birthday month the caller said, as the full month name in English, e.g. December",
  1280 |     );
  1281 | 
  1282 |     // -------------------------------------------------------
  1283 |     // Only December passes
  1284 |     // -------------------------------------------------------
  1285 | 
  1286 |     const patternInput = dialog.getByRole("textbox", {
  1287 |       name: "Pattern (regex)",
  1288 |     });
  1289 | 
  1290 |     const decemberPattern = "^[Dd][Ee][Cc][Ee][Mm][Bb][Ee][Rr]$";
  1291 | 
  1292 |     await patternInput.fill(decemberPattern);
  1293 | 
  1294 |     await expect(patternInput).toHaveValue(decemberPattern);
  1295 | 
  1296 |     console.log("Input source = Let the agent decide, Pattern = December");
  1297 |   }
  1298 | 
  1299 |   // =========================================================
  1300 |   // TEST VALUE TYPE OPTIONS
  1301 |   // =========================================================
  1302 | 
  1303 |   async verifyDataValidatorValueTypes() {
  1304 |     const dialog = this.page.getByRole("dialog");
  1305 | 
  1306 |     // -------------------------------------------------------
  1307 |     // String -> Number
  1308 |     // -------------------------------------------------------
```