# Accuknox-user-management-tests
import { test } from "@playwright/test";
import { LoginPage } from "../pages/login.page";
import { AdminPage } from "../pages/admin.page";

test("Delete user", async ({ page }) => {
  const login = new LoginPage(page);
  const admin = new AdminPage(page);

  await page.goto("https://opensource-demo.orangehrmlive.com/");
  await login.login("Admin", "admin123");

  await admin.navigateToAdmin();
  await admin.searchUser("testuser01");

  await page.getByRole("checkbox").check();
  await page.getByRole("button", { name: "Delete" }).click();
  await page.getByRole("button", { name: "Yes, Delete" }).click();

  await page.waitForSelector("text=Success");
});


/////////////////////////////////////////////////

import { test } from "@playwright/test";
import { LoginPage } from "../pages/login.page";
import { AdminPage } from "../pages/admin.page";

test("Edit user", async ({ page }) => {
  const login = new LoginPage(page);
  const admin = new AdminPage(page);

  await page.goto("https://opensource-demo.orangehrmlive.com/");
  await login.login("Admin", "admin123");

  await admin.navigateToAdmin();
  await admin.searchUser("testuser01");

  await page.getByRole("button", { name: "Edit" }).click();
  await page.getByLabel("Status").selectOption("Disabled");

  await admin.saveBtn.click();

  await page.waitForSelector("text=Success");
});

////////////////////////////////////////////////////////

[10:09 pm, 2/12/2025] Dhale Rakshita 🤍: import { test } from "@playwright/test";
import { LoginPage } from "../pages/login.page";
import { AdminPage } from "../pages/admin.page";

test("Search user", async ({ page }) => {
  const login = new LoginPage(page);
  const admin = new AdminPage(page);

  await page.goto("https://opensource-demo.orangehrmlive.com/");
  await login.login("Admin", "admin123");

  await admin.navigateToAdmin();
  await admin.searchUser("testuser01");

  await page.waitForSelector("text=testuser01");
});

//////////////////////////////////////////////////////////////////////
import { test } from "@playwright/test";
import { LoginPage } from "../pages/login.page";
import { AdminPage } from "../pages/admin.page";

test("Add new user", async ({ page }) => {
  const login = new LoginPage(page);
  const admin = new AdminPage(page);

  await page.goto("https://opensource-demo.orangehrmlive.com/");
  await login.login("Admin", "admin123");

  await admin.navigateToAdmin();
  await admin.addBtn.click();

  await page.getByLabel("Employee Name").fill("Paul Collings");
  await page.getByLabel("Username").fill("testuser01");
  await page.getByLabel("Password").fill("Test@1234");
  await page.getByLabel("Confirm Password").fill("Test@1234");

  await admin.saveBtn.click();

  await page.waitForSelector("text=Success");
});
////////////////////////////////////////////////////////////
 import { Page } from "@playwright/test";
 export class AdminPage {
  constructor(private page: Page) {}

  adminMenu = this.page.getByRole("link", { name: "Admin" });
  addBtn = this.page.getByRole("button", { name: "Add" });
  searchUsername = this.page.getByPlaceholder("Username");
  saveBtn = this.page.getByRole("button", { name: "Save" });

  async navigateToAdmin() {
    await this.adminMenu.click();
  }

  async searchUser(username: string) {
    await this.searchUsername.fill(username);
    await this.page.getByRole("button", { name: "Search" }).click();
  }
}
/////////////////////////////////////////////////////////////////////
import { Page } from "@playwright/test";
export class LoginPage {
constructor(private page: Page) {}

  username = this.page.getByPlaceholder("Username");
  password = this.page.getByPlaceholder("Password");
  loginBtn = this.page.getByRole("button", { name: "Login" });

  async login(user: string, pass: string) {
    await this.username.fill(user);
    await this.password.fill(pass);
    await this.loginBtn.click();
  }
}
# OrangeHRM User Management Automation
/////////////////////////////////////////////////////////////////////////
 
 import { defineConfig } from "@playwright/test";

export default defineConfig({
  testDir: "./tests",
  timeout: 30 * 1000,
  retries: 0,
  use: {
    headless: true,
    screenshot: "only-on-failure",
    video: "retain-on-failure",
    viewport: { width: 1280, height: 720 }
  },
  reporter: [["html", { open: "never" }]],
});


