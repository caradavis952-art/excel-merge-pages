# Excel Batch Merge Tool / Excel 批量合并工具

A single-file, fully client-side web tool for batch-merging Excel files. Deploy as a GitHub Pages static site — no backend, no build step, files never leave the browser.

单文件、纯浏览器端的 Excel 批量合并工具，可直接部署为 GitHub Pages 静态页面——无后端、无构建步骤，文件不会上传到任何服务器。

**Live demo:** `https://<your-username>.github.io/<repo-name>/`

## Features / 功能

- **Auto header detection & grouping** — files with identical headers are merged together; files with different headers are merged group by group, each group downloadable separately. / 表头完全相同的文件自动合并；不同表头按组分别合并、分别下载
- **Merge by union of headers** (optional) — merges all files into one using the union of every header, leaving missing cells empty. / 按表头并集合并（可选）：以所有表头并集为准，缺失单元格留空
- **Source file column** (optional) — appends a `Source File` column with the plain file name each row came from (no `.xlsx` extension, no folder path for files inside zips). / 末列填充源文件名（可选）：纯文件名，不含后缀与 zip 内文件夹路径
- **Drag-and-drop, multi-select, or one-by-one upload** — mix and match; merge when ready. / 拖拽 / 多选 / 逐个上传均可，选完再合并
- **.zip archives** — auto-extracted, nested folders supported, `.xlsx` inside are merged (junk entries like `__MACOSX` / `.DS_Store` / `~$` temp files are skipped). / zip 自动解压（支持多级文件夹，自动跳过 macOS 垃圾文件与 Office 临时文件）
- **Cell overflow handling** — text exceeding the Excel cell limit (32,767 chars) is truncated with a trailing `...` and a "Text too long, truncated" comment on the cell; the page reports how many cells were truncated. Excel (.xlsx) download only. / 超长文本截断至 32767 字符并以 "..." 结尾，单元格加批注，页面提示截断数量；仅提供 xlsx 下载
- **Naming** — default file name joins the source file names (`FileA_FileB.xlsx`); custom names supported. / 默认源文件名拼接命名，支持自定义
- **EN / 中文 interface** — toggle at the top right; the choice is remembered per browser. Generated file content (comments, source column name, sheet name) follows the interface language. / 中英界面切换，输出文件内容随界面语言
- Only the **first worksheet** of each file is read. / 仅读取每个文件的第一个工作表

## Deploy / 部署

1. Create a **public** repository. / 新建一个公开仓库
2. Push the contents of this folder (at least `index.html`) to the `main` branch root. / 将本目录内容（至少 `index.html`）推送到 `main` 分支根目录
3. Repo **Settings → Pages → Deploy from a branch** → branch `main`, folder `/ (root)`, save. Wait ~1 minute. / 仓库设置 → Pages → 从分支部署，选 `main` / 根目录，保存后约 1 分钟生效
4. Open `https://<your-username>.github.io/<repo-name>/`. / 打开上面的地址即可使用

For a project-site at `https://<user>.github.io/<repo>/`, this folder is ready as-is. If you want it at your user-site root instead, same steps on `<user>.github.io` repo.

## Notes / 说明

- ExcelJS and JSZip are loaded from public CDNs (jsDelivr → unpkg → npmmirror, with automatic fallback), so **internet access is required** on first load. If all CDNs fail, the page shows a banner asking to refresh. / ExcelJS / JSZip 从公共 CDN 加载（三源自动回退），首次打开需联网；全部源失败时页面会显示提示
- Everything runs locally: parsing, merging, and file generation all happen in your browser. / 解析、合并、生成文件全部在浏览器本地完成

## Local Development / 本地开发

No build step. Open `index.html` directly in a browser, or serve it:

```
python -m http.server 8000
# then visit http://localhost:8000/
```

## License

MIT — do whatever you like, attribution appreciated.
