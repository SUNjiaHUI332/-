<template>
  <div id="app">
    <div v-if="!isLoggedIn" class="login-container">
      <div class="login-box">
        <h2>PDF题在线转换系统</h2>
        <div class="form-group">
          <label>用户名：</label>
          <input v-model="username" type="text" class="form-input" />
        </div>
        <div class="form-group">
          <label>密码：</label>
          <input v-model="password" type="password" class="form-input" />
        </div>
        <button class="login-button" @click="handleLogin">登录</button>
      </div>
    </div>
    <div v-else>
      <div class="upload-container">
        <div class="upload-wrapper">
          <label class="upload-button">
            <span class="upload-icon">📄</span>
            <span class="upload-text">选择PDF文件</span>
            <input
              type="file"
              @change="handleFileUpload"
              accept="application/pdf"
            />
          </label>
          <div class="action-buttons">
            <button class="export-button" @click="exportToXLSX">
              <span class="icon">📤</span> 导出XLSX
            </button>
            <button
              class="batch-edit-button"
              @click="showBatchEditModal = true"
            >
              <span class="icon">✏️</span> 批量编辑
            </button>
          </div>
          <div class="conversion-system">
            <h3>PDF题在线转换系统</h3>
            <div class="system-info">
              <p>
                文件：<span class="status">{{ fileName }}</span>
              </p>
            </div>
            <div class="system-info">
              <p>当前状态：<span class="status">运行中</span></p>
            </div>
          </div>
        </div>
      </div>
      <div class="table-container" v-if="parsedData.length">
        <el-table height="650" :data="parsedData" style="width: 100%">
          <el-table-column
            type="index"
            label="序号"
            width="80"
            :align="`center`"
          />

          <el-table-column
            prop="course"
            label="课程"
            width="200"
            :align="`center`"
          >
            <template #default="{ row }">
              <el-input v-model="row.course" />
            </template>
          </el-table-column>
          <el-table-column
            prop="unit"
            label="单元"
            width="200"
            :align="`center`"
          >
            <template #default="{ row }">
              <el-input v-model="row.unit" />
            </template>
          </el-table-column>
          <el-table-column
            prop="type"
            label="题目类型"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="content"
            label="题目内容"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="answer"
            label="正确答案"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="analysis"
            label="解析"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="image"
            label="配图"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="option1"
            label="选项1"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="option2"
            label="选项2"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="option3"
            label="选项3"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="option4"
            label="选项4"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="option5"
            label="选项5"
            width="200"
            :align="`center`"
          />
          <el-table-column
            prop="option6"
            label="选项6"
            width="200"
            :align="`center`"
          />

          <el-table-column
            prop="option7"
            label="选项7"
            width="200"
            :align="`center`"
          />

          <el-table-column
            prop="option8"
            label="选项8"
            width="200"
            :align="`center`"
          />
        </el-table>
      </div>

      <!-- 批量编辑模态框 -->
      <div v-if="showBatchEditModal" class="modal-overlay">
        <div class="modal-content">
          <h3>批量编辑</h3>
          <div class="form-group">
            <label>课程：</label>
            <input v-model="batchCourse" class="form-input" />
          </div>
          <div class="form-group">
            <label>单元：</label>
            <input v-model="batchUnit" class="form-input" />
          </div>
          <div class="modal-actions">
            <button class="confirm-button" @click="applyBatchEdit">确认</button>
            <button class="cancel-button" @click="showBatchEditModal = false">
              取消
            </button>
          </div>
        </div>
      </div>

      <div v-if="isUploading" class="uploading-overlay">
        <div class="uploading-spinner"></div>
        <div class="uploading-text">正在上传并解析PDF文件，请稍候...</div>
      </div>
    </div>
  </div>
</template>

<script>
import * as pdfjsLib from "pdfjs-dist/build/pdf";
import pdfjsWorker from "pdfjs-dist/build/pdf.worker.entry";
import * as XLSX from "xlsx";

export default {
  name: "App",
  data() {
    return {
      parsedData: [],
      showBatchEditModal: false,
      batchCourse: "",
      batchUnit: "",
      isUploading: false,
      isLoggedIn: true,
      username: "PDF题在线转换系统",
      password: "123456",
      fileName: "",
    };
  },
  mounted() {
    // this.setupColumnResize();
  },
  methods: {
    handleLogin() {
      // 简单验证
      if (this.username === "PDF题在线转换系统" && this.password === "123456") {
        this.isLoggedIn = true;
      } else {
        alert("用户名或密码错误");
      }
    },
    async handleFileUpload(event) {
      this.isUploading = true;
      const file = event.target.files[0];
      this.fileName = file ? file.name : "未选择文件"; // 存储文件名

      setTimeout(async () => {
        this.isUploading = false;
        const file = event.target.files[0];
        if (file) {
          const arrayBuffer = await file.arrayBuffer();

          pdfjsLib.GlobalWorkerOptions.workerSrc = pdfjsWorker;

          try {
            const loadingTask = pdfjsLib.getDocument({
              data: arrayBuffer,
              disableAutoFetch: true,
              disableStream: true,
            });

            const pdfDoc = await loadingTask.promise;
            const numPages = pdfDoc.numPages;

            let allText = "";
            for (let i = 1; i <= numPages; i++) {
              const page = await pdfDoc.getPage(i);
              const textContent = await page.getTextContent();
              allText +=
                textContent.items.map((item) => item.str).join("\n") + "\n";
            }

            const filteredText = allText
              .replace(/羿过教育官网 www\.yiguojy\.com 版权所有/g, "")
              .replace(
                /专业网校课程、题库软件、考试用书、资讯信息全方位一体化职业考试学习平台/g,
                ""
              );

            const questions = filteredText.split(/(?=\d+\.)/g);
            const parsed = [];

            questions.forEach((question) => {
              const lines = question.split("\n").filter((line) => line.trim());
              if (lines.length >= 3) {
                const options = lines
                  .slice(1, -2)
                  .filter(
                    (line) =>
                      !line.startsWith("参考答案") && !line.startsWith("【")
                  )
                  .map((opt) => opt.trim());

                const analysisStartIndex = lines.findIndex((line) =>
                  line.startsWith("【羿过解析】")
                );

                console.log(analysisStartIndex, "解析啊");

                var analysisText = lines
                  .slice(analysisStartIndex)
                  .join("\n")
                  .split("【羿过解析】")[1];
                if (/\d$/.test(analysisText)) {
                  analysisText = analysisText.slice(0, -1);
                }
                // console.log(analysisText,'看我啊');
                if (analysisText) {
                  if (analysisText.endsWith("问答题")) {
                    analysisText = analysisText.slice(0, -3);
                  }
                }
                const optionMap = {
                  A: "option1",
                  B: "option2",
                  C: "option3",
                  D: "option4",
                  E: "option5",
                  F: "option6",
                  G: "option7",
                  H: "option8",
                };

                const parsedOptions = {};
                options.forEach((opt) => {
                  const match = opt.match(/^([A-H])\.\s*(.*)/);
                  if (match) {
                    const [, key, value] = match;
                    // console.log(value, "valuevalue");
                    parsedOptions[optionMap[key]] = value;
                  }
                });
                const answerLine1 = lines.find((line) =>
                  line.startsWith("参考答案：")
                );
                const answerText2 = answerLine1
                  ? answerLine1.split("参考答案：")[1]
                  : "";

                // 处理题目内容
                let questionContent = "";
                for (let i = 0; i < lines.length; i++) {
                  const line = lines[i];
                  if (line.startsWith("A.")) {
                    // 获取A.前面的所有行作为题目内容
                    questionContent = lines
                      .slice(0, i)
                      .join("")
                      .replace(/^\d+\./, ""); // 去掉前面的序号
                    break;
                  }

                  if (
                    line.endsWith("。") ||
                    line.endsWith("）") ||
                    line.endsWith("问：") ||
                    /^\(\d+\)/.test(line)
                  ) {
                    questionContent += line.replace(/^\d+\./, ""); // 去掉前面的序号
                    if (
                      line.endsWith("。") ||
                      line.endsWith("）") ||
                      line.endsWith("问：")
                    ) {
                      break;
                    }
                  } else {
                    questionContent += line.replace(/^\d+\./, ""); // 去掉前面的序号
                  }
                }

                // 题目内容处理
                // const finalContent = 222;

                parsed.push({
                  course: "专升本-法学类",
                  unit: "民法",
                  type: "单选题",
                  content: questionContent,
                  answer: answerText2,
                  analysis: analysisText,
                  image: "",
                  option1: parsedOptions.option1 || "",
                  option2: parsedOptions.option2 || "",
                  option3: parsedOptions.option3 || "",
                  option4: parsedOptions.option4 || "",
                  option5: parsedOptions.option5 || "",
                  option6: parsedOptions.option6 || "",
                  option7: parsedOptions.option7 || "",
                  option8: parsedOptions.option8 || "",
                });
              }
            });

            this.parsedData = parsed;
          } catch (error) {
            console.error("PDF解析失败:", error);
          }
        }
      }, 1500);
    },
    exportToXLSX() {
      if (this.parsedData.length === 0) {
        alert("没有数据可以导出！");
        return;
      }

      const headers = {
        course: "课程",
        unit: "单元",
        type: "题目类型",
        content: "题目内容",
        answer: "正确答案",
        analysis: "解析",
        image: "配图",
        option1: "选项1",
        option2: "选项2",
        option3: "选项3",
        option4: "选项4",
        option5: "选项5",
        option6: "选项6",
        option7: "选项7",
        option8: "选项8",
      };

      const dataWithHeaders = this.parsedData.map((item) => {
        const newItem = {};
        for (const key in item) {
          newItem[headers[key]] = item[key];
        }
        return newItem;
      });

      const worksheet = XLSX.utils.json_to_sheet(dataWithHeaders);
      const workbook = XLSX.utils.book_new();
      XLSX.utils.book_append_sheet(workbook, worksheet, "Sheet1");

      const exportFileName = this.fileName
        ? this.fileName.replace(".pdf", ".xlsx")
        : "export.xlsx";
      // XLSX.writeFile(workbook, exportFileName);
      XLSX.writeFile(workbook, exportFileName);
    },
    applyBatchEdit() {
      this.parsedData.forEach((item) => {
        if (this.batchCourse) item.course = this.batchCourse;
        if (this.batchUnit) item.unit = this.batchUnit;
      });
      this.showBatchEditModal = false;
    },
  },
};
</script>

<style>
.table-container {
  margin: 20px;
}
.system-info {
  margin-top: 10px;
}
body {
  padding: auto;
  margin: auto;
}
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.login-box {
  background-color: rgba(255, 255, 255, 0.9);
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
  width: 350px;
}
/* 新增登录界面样式 */
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f5f5f5;
}

.login-box {
  background-color: white;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  width: 350px;
}

.login-box h2 {
  text-align: center;
  margin-bottom: 20px;
}

.login-button {
  width: 100%;
  padding: 10px;
  background-color: #409eff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.login-button:hover {
  background-color: #66b1ff;
}

/* 新增样式 */
.uploading-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, 0.9);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.uploading-spinner {
  border: 4px solid #f3f3f3;
  border-top: 4px solid #409eff;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 1s linear infinite;
}

.uploading-text {
  margin-top: 15px;
  font-size: 16px;
  color: #333;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.system-info p {
  margin: 8px 0;
  font-size: 14px;
}

.status {
  color: #28a745;
  font-weight: bold;
}

.count {
  color: #007bff;
  font-weight: bold;
}

.rate {
  color: #ffc107;
  font-weight: bold;
}

.action-buttons {
  display: flex;
  gap: 10px;
  margin-left: 10px;
}

.upload-container {
  margin-bottom: 30px;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 8px;
}

.upload-wrapper {
  display: flex;
  align-items: center;
  gap: 20px;
  justify-content: space-between;
}

.upload-button {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 24px;
  background-color: #409eff;
  color: white;
  border-radius: 6px;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
}

.upload-button:hover {
  background-color: #66b1ff;
  transform: translateY(-2px);
}

.upload-icon {
  font-size: 18px;
}

.upload-text {
  font-size: 14px;
}

.upload-button input[type="file"] {
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0;
  cursor: pointer;
  left: 0;
  top: 0;
}

.action-buttons {
  display: flex;
  gap: 10px;
}
.export-button,
.batch-edit-button {
  display: flex;
  align-items: center;
  gap: 5px;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.export-button {
  background-color: #28a745;
  color: white;
}

.batch-edit-button {
  background-color: #ffc107;
  color: black;
}

.export-button:hover {
  background-color: #218838;
}

.batch-edit-button:hover {
  background-color: #e0a800;
}

.editable-input {
  width: 100%;
  padding: 5px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  width: 400px;
}

.form-group {
  margin-bottom: 15px;
}

.form-input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}

.confirm-button {
  background-color: #28a745;
  color: white;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.cancel-button {
  background-color: #dc3545;
  color: white;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.confirm-button:hover {
  background-color: #218838;
}

.cancel-button:hover {
  background-color: #c82333;
}

/* 表格样式优化 */
table {
  width: 100%;
  border-collapse: collapse;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  table-layout: fixed; /* 固定表格布局 */
}

th,
td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: center;
  font-size: 12px;
  word-wrap: break-word; /* 允许单词换行 */
  white-space: normal; /* 允许内容换行 */
}

th {
  background-color: #409eff;
  color: #000;
  position: sticky;
  top: 0;
  z-index: 1;
}

tr:nth-child(even) {
  background-color: #f9f9f9;
}

tr:hover {
  background-color: #f1f1f1;
}

.editable-input {
  width: 90%;
  padding: 5px;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
}
</style>