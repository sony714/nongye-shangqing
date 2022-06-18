<template>
  <div class="container">
    <header>
      <div class="sweather">
        <iframe
          allowtransparency="true"
          frameborder="0"
          width="575"
          height="96"
          scrolling="no"
          src="//tianqi.2345.com/plugin/widget/index.htm?s=1&z=1&t=0&v=0&d=5&bd=0&k=000000&f=ffffff&ltf=009944&htf=cc0000&q=0&e=1&a=1&c=57494&w=575&h=96&align=center"
        ></iframe>
      </div>
      <h1>良顷种植环境信息测报平台</h1>
      <div class="time"></div>
    </header>
    <main>
      <div class="stations">
        <div class="stations-select">
          <ul>
            <li style="background-color: #132e78">动态监测信息</li>
            <li
              :class="key === 0 ? 'selected' : ''"
              @click="
                () => {
                  (key = 0), this.init();
                }
              "
            >
              墒情信息
            </li>
            <li
              :class="key === 1 ? 'selected' : ''"
              @click="
                () => {
                  key = 1;
                  if (this.myChart) {
                    this.myChart.clear();
                  }
                }
              "
            >
              长势信息
            </li>
            <li
              :class="key === 2 ? 'selected' : ''"
              @click="
                () => {
                  (key = 2), this.initInsect();
                }
              "
            >
              虫情信息
            </li>
          </ul>
        </div>
        <div class="section" v-if="key === 0">
          <dv-border-box-10 style="width: 31.5%">
            <div class="section-item">
              <h3>实时信息</h3>
              <div class="table">
                <div class="table-item">
                  <div class="table-item-title">风速</div>
                  <div class="table-item-value">
                    {{ realInfo.e1 | capitalize }} m/s
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">雨量</div>
                  <div class="table-item-value">{{ realInfo.e2 }}mm</div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">大气温度</div>
                  <div class="table-item-value">
                    {{ realInfo.e3 | capitalize }} ℃
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">雨量累计</div>
                  <div class="table-item-value">{{ realInfo.e4 }} mm</div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">数字气压</div>
                  <div class="table-item-value">
                    {{ realInfo.e5 | capitalize }} hPa
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">简易总辐射</div>
                  <div class="table-item-value">{{ realInfo.e6 }} W/m2</div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">风向</div>
                  <div class="table-item-value">
                    {{ realInfo.e7 }} ° 西南偏西
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">辐射累计</div>
                  <div class="table-item-value">
                    {{ realInfo.e8 / 100 }} MJ/m2
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">大气湿度</div>
                  <div class="table-item-value">
                    {{ realInfo.e9 | capitalize }} %RH
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">照度</div>
                  <div class="table-item-value">
                    {{ realInfo.e10 * 10 }} Lux
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">土温1</div>
                  <div class="table-item-value">
                    {{ realInfo.e11 | capitalize }} ℃
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">土湿1</div>
                  <div class="table-item-value">
                    {{ realInfo.e12 | capitalize }}%
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">土温2</div>
                  <div class="table-item-value">
                    {{ realInfo.e13 | capitalize }} ℃
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">土湿2</div>
                  <div class="table-item-value">
                    {{ realInfo.e14 | capitalize }} %
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">土温3</div>
                  <div class="table-item-value">
                    {{ realInfo.e15 | capitalize }} ℃
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">土湿3</div>
                  <div class="table-item-value">
                    {{ realInfo.e16 | capitalize }} %
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">土温4</div>
                  <div class="table-item-value">
                    {{ realInfo.e17 | capitalize }} ℃
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">土湿4</div>
                  <div class="table-item-value">
                    {{ realInfo.e18 | capitalize }} %
                  </div>
                </div>
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10 style="width: 31%">
            <div class="section-item">
              <h3 class="section-item-title">搜索信息</h3>
              <div class="realTime">
                <div class="content">
                  <el-table
                    :data="tableData"
                    height="26rem"
                    :cell-style="rowClass"
                  >
                    <el-table-column
                      fixed
                      prop="dataTime"
                      label="日期"
                      width="160"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      prop="e1"
                      label="风速(m/s)"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="雨量(mm)"
                      prop="e2"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="大气温度(℃)"
                      prop="e3"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="雨量累计(mm)"
                      prop="e4"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="数字气压(hPa)"
                      prop="e5"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="简易总辐射(W/m2)"
                      prop="e6"
                      width="140"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="风向(°)"
                      prop="e7"
                      width="140"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="辐射累计(MJ/m2)"
                      prop="e8"
                      width="160"
                      header-align="center"
                      algin="center"
                    />
                    <el-table-column
                      label="大气湿度(%RH)"
                      prop="e9"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="照度(Lux)"
                      prop="e10"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="土温1(℃)"
                      prop="e11"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="土湿1(%)"
                      prop="e12"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="土温2(℃)"
                      prop="e13"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="土湿2(%)"
                      prop="e14"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="土温3(℃)"
                      prop="e15"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="土湿3(%)"
                      prop="e16"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="土温4(℃)"
                      prop="e17"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="土湿4(%)"
                      prop="e18"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                  </el-table>
                </div>
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10 style="width: 31%; margin-right: 10px">
            <div class="section-item">
              <h3 class="section-item-title">统计信息</h3>
              <div ref="reference" style="width: 100%; height: 26rem"></div>
            </div>
          </dv-border-box-10>
        </div>
        <div class="section1" v-else-if="key === 1">
          <dv-border-box-10>
            <div class="section1-item">
              <h3>播种期</h3>
              <div class="image">
                <el-carousel height="150px" style="width:200px" indicator-position="outside">
                  <el-carousel-item>
                      <img src="../assets/image/1.png" alt="" />
                  </el-carousel-item>
                  <el-carousel-item>
                      <img src="../assets/image/2.png" alt="" />
                  </el-carousel-item>
                  <el-carousel-item>
                      <img src="../assets/image/3.png" alt="" />
                  </el-carousel-item>
                  <el-carousel-item>
                      <img src="../assets/image/4.png" alt="" />
                  </el-carousel-item>
                  <el-carousel-item>
                      <img src="../assets/image/5.png" alt="" />
                  </el-carousel-item>
                </el-carousel>
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10>
            <div class="section1-item">
              <h3>出苗期</h3>
              <div class="image">
               <el-carousel height="150px" style="width:200px" indicator-position="outside">
                  <el-carousel-item>
                      <img src="../assets/image/6.png" alt="" />
                  </el-carousel-item>
                  <el-carousel-item>
                      <img src="../assets/image/7.png" alt="" />
                  </el-carousel-item>
                  <el-carousel-item>
                      <img src="../assets/image/8.png" alt="" />
                  </el-carousel-item>
                  <el-carousel-item>
                      <img src="../assets/image/10.png" alt="" />
                  </el-carousel-item>
                </el-carousel>
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10>
            <div class="section1-item">
              <h3>追肥期</h3>
              <div class="image">
                <img src="../assets/image/11.png" alt="" />
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10>
            <div class="section1-item">
              <h3>抽雄期</h3>
              <div class="image">
                <img src="../assets/image/13.png" alt="" />
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10>
            <div class="section1-item">
              <h3>吐丝期</h3>
              <div class="image">
                <img src="../assets/image/21.png" alt="" />
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10>
            <div class="section1-item">
              <h3>成熟期</h3>
              <div class="image">
                <img src="../assets/image/30.png" alt="" />
              </div>
            </div>
          </dv-border-box-10>
        </div>
        <section class="section" v-else>
          <dv-border-box-10 style="width: 31%">
            <div class="section-item">
              <h3>设备运行</h3>
              <div class="table" style="margin-top: 1rem">
                <div class="table-item">
                  <div class="table-item-title">电源电压</div>
                  <div class="table-item-value">
                    {{ insectInfo.e1 / 1000 }} V
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">管道温度</div>
                  <div class="table-item-value">{{ insectInfo.e2 / 10 }}℃</div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">照度</div>
                  <div class="table-item-value">
                    {{ insectInfo.e3 * 100 }} Lux
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">运行模式</div>
                  <div class="table-item-value">{{ insectInfo.e4 }} mm</div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">虫仓号</div>
                  <div class="table-item-value">
                    {{ insectInfo.e5 }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">错误码</div>
                  <div class="table-item-value">{{ insectInfo.e6 }}</div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">当前电机</div>
                  <div class="table-item-value">旋转仓</div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">电机方向</div>
                  <div class="table-item-value">正转</div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">经度</div>
                  <div class="table-item-value">
                    {{ insectInfo.e9 / 1000000 }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">纬度</div>
                  <div class="table-item-value">
                    {{ insectInfo.e10 / 10000 }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">室外温度</div>
                  <div class="table-item-value">
                    {{ insectInfo.e13 | capitalize }} ℃
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">进入低温休眠</div>
                  <div class="table-item-value">
                    {{ insectInfo.e15 }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">低温休眠开关</div>
                  <div class="table-item-value">
                    {{ insectInfo.e16 }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">加热</div>
                  <div class="table-item-value">
                    {{ insectInfo.e17 === 0 ? "关" : "开" }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">诱虫</div>
                  <div class="table-item-value">
                    {{ insectInfo.e18 === 0 ? "关" : "开" }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">补光</div>
                  <div class="table-item-value">
                    {{ insectInfo.e19 === 0 ? "关" : "开" }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">屏幕电源</div>
                  <div class="table-item-value">
                    {{ insectInfo.e20 === 0 ? "关" : "开" }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">振动</div>
                  <div class="table-item-value">
                    {{ insectInfo.e21 === 0 ? "关" : "开" }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">上虫仓</div>
                  <div class="table-item-value">
                    {{ insectInfo.e22 === 0 ? "关" : "开" }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">下虫仓</div>
                  <div class="table-item-value">
                    {{ insectInfo.e23 === 0 ? "关" : "开" }}
                  </div>
                </div>
                <div class="table-item">
                  <div class="table-item-title">传送带</div>
                  <div class="table-item-value">
                    {{ insectInfo.e24 === 0 ? "关" : "开" }}
                  </div>
                </div>
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10 style="width: 31%">
            <div class="section-item">
              <h3 class="section-item-title">搜索信息</h3>
              <div class="realTime">
                <div class="content">
                  <el-table
                    :data="tableData2"
                    style="width: 554px"
                    height="26rem"
                    :cell-style="rowClass"
                  >
                    <el-table-column
                      fixed
                      prop="dataTime"
                      label="日期"
                      width="160"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      prop="e1"
                      label="电源电压"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      prop="e2"
                      label="管道温度(℃)"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="照度(Lux)"
                      prop="e3"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="运行模式()"
                      prop="e4"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="虫仓号()"
                      prop="e5"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="错误码()"
                      prop="e6"
                      width="120"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="当前电机()"
                      prop="e7"
                      width="140"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="电机方向()"
                      prop="e8"
                      width="140"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="经度()"
                      prop="e9"
                      width="160"
                      header-align="center"
                      algin="center"
                    />
                    <el-table-column
                      label="纬度()"
                      prop="e10"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="室外温度(℃)"
                      prop="e13"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="进入低温休眠"
                      prop="e14"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="低温休眠开关"
                      prop="e15"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="加热"
                      prop="e16"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="诱虫"
                      prop="e17"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="补光"
                      prop="e18"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="屏幕电源"
                      prop="e19"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="振动"
                      prop="e20"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="上虫仓"
                      prop="e21"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="下虫仓"
                      prop="e22"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                    <el-table-column
                      label="传送带"
                      prop="e23"
                      width="80"
                      algin="center"
                      header-align="center"
                    />
                  </el-table>
                </div>
              </div>
            </div>
          </dv-border-box-10>
          <dv-border-box-10 style="width: 31%; margin-right: 10px">
            <div class="section-item">
              <h3 class="section-item-title">虫情图片</h3>
              <div ref="reference2" class="pic">
                <div
                  class="pic-item"
                  v-for="(item, index) in picList"
                  :key="index"
                >
                  <div class="pic-item-image">
                    <el-image
                      :src="item.image"
                      fit="contain"
                      style="width:100%;height=100%"
                    ></el-image>
                  </div>
                  <div class="pic-item-info">
                    <div class="pic-item-time">{{ item.dataTime }}</div>
                    <div class="pic-item-classes">
                      <span>种类:{{ item.result.kind }}</span
                      ><span>数量:{{ item.result.total }}</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </dv-border-box-10>
        </section>
      </div>
      <div class="analysis">
        <div class="analysis-first">种植决策分析</div>
        <dv-border-box-1>
          <div class="analysis-item">
            <h3>墒情分析</h3>
            <ol>
              <li>播种期</li>
              <li>出苗期</li>
              <li>追肥期</li>
              <li>抽雄期</li>
              <li>吐丝期</li>
              <li>成熟期</li>
            </ol>
          </div>
        </dv-border-box-1>
        <dv-border-box-1>
          <div class="analysis-item">
            <h3>作物长势分析</h3>
            <ol>
              <li>播种期</li>
              <li>出苗期</li>
              <li>追肥期</li>
              <li>抽雄期</li>
              <li>吐丝期</li>
              <li>成熟期</li>
            </ol>
          </div>
        </dv-border-box-1>
        <dv-border-box-1>
          <div class="analysis-item">
            <h3>施肥浇水分析</h3>
            <ol>
              <li>出苗期</li>
              <li>追肥期</li>
              <li>抽雄期</li>
              <li>吐丝期</li>
              <li>成熟期</li>
            </ol>
          </div>
        </dv-border-box-1>
        <dv-border-box-1>
          <div class="analysis-item">
            <h3>植保虫情分析</h3>
            <ol>
              <li>播种期</li>
              <li>出苗期</li>
              <li>追肥期</li>
              <li>抽雄期</li>
              <li>吐丝期</li>
              <li>成熟期</li>
            </ol>
          </div>
        </dv-border-box-1>
      </div>
    </main>
  </div>
</template>

<script>
const axios = require("axios");
import * as echarts from "echarts";
export default {
  name: "Base",
  data() {
    return {
      key: 0,
      tableData: [],
      token: "",
      myChart: "",
      realInfo: "",
      insectInfo: "",
      tableData2: [],
      weatherList: [], //天气列表
      picList: [],
    };
  },
  filters: {
    capitalize: function (value) {
      if (!value) return "";
      value = value / 10;
      return value;
    },
  },
  methods: {
    draw(dataTime, obj) {
      this.myChart = echarts.init(this.$refs.reference);
      let option = {
        tooltip: {
          trigger: "axis",
          position: ["50%", "20%"],
        },
        grid: {
          show: true,
          bottom: 60,
        },
        dataZoom: {
          type: "slider",
          height: 38,
          start: 0,
          end: 50,
          bottom: "-15px",
        },
        axisLabel: {
          color: "#fff",
        },
        legend: {
          data: [
            "风速",
            "雨量",
            "大气温度",
            "雨量累计",
            "数字气压",
            "简易总辐射",
            "风向",
            "辐射累计",
            "大气湿度",
            "照度",
            "土温1",
            "土湿1",
            "土温2",
            "土湿2",
            "土温3",
            "土湿3",
            "土温4",
            "土湿4",
          ],
          textStyle: {
            color: "#fff",
          },
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true,
        },
        toolbox: {
          feature: {
            saveAsImage: {},
          },
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: dataTime,
        },
        yAxis: {
          type: "value",
        },
        series: [
          {
            name: "风速",
            type: "line",
            stack: "Total",
            data: obj.e1,
          },
          {
            name: "雨量",
            type: "line",
            stack: "Total",
            data: obj.e2,
          },
          {
            name: "大气温度",
            type: "line",
            stack: "Total",
            data: obj.e3,
          },
          {
            name: "雨量累计",
            type: "line",
            stack: "Total",
            data: obj.e4,
          },
          {
            name: "数字气压",
            type: "line",
            stack: "Total",
            data: obj.e5,
          },
          {
            name: "简易总辐射",
            type: "line",
            stack: "Total",
            data: obj.e6,
          },
          {
            name: "风向",
            type: "line",
            stack: "Total",
            data: obj.e7,
          },
          {
            name: "辐射累计",
            type: "line",
            stack: "Total",
            data: obj.e8,
          },
          {
            name: "大气湿度",
            type: "line",
            stack: "Total",
            data: obj.e9,
          },
          {
            name: "照度",
            type: "line",
            stack: "Total",
            data: obj.e10,
          },
          {
            name: "土温1",
            type: "line",
            stack: "Total",
            data: obj.e11,
          },
          {
            name: "土湿1",
            type: "line",
            stack: "Total",
            data: obj.e12,
          },
          {
            name: "土温2",
            type: "line",
            stack: "Total",
            data: obj.e13,
          },
          {
            name: "土湿2",
            type: "line",
            stack: "Total",
            data: obj.e14,
          },
          {
            name: "土温3",
            type: "line",
            stack: "Total",
            data: obj.e15,
          },
          {
            name: "土湿3",
            type: "line",
            stack: "Total",
            data: obj.e16,
          },
          {
            name: "土温4",
            type: "line",
            stack: "Total",
            data: obj.e17,
          },
          {
            name: "土湿4",
            type: "line",
            stack: "Total",
            data: obj.e18,
          },
        ],
      };
      option && this.myChart.setOption(option);
    },
    draw2(dataTime, obj) {
      const myChart = echarts.init(this.$refs.reference2);
      let option = {
        tooltip: {
          trigger: "axis",
          position: ["50%", "20%"],
        },
        grid: {
          show: true,
          bottom: 60,
        },
        dataZoom: {
          type: "slider",
          height: 28,
          start: 0,
          end: 50,
          bottom: "-15px",
        },
        axisLabel: {
          color: "#fff",
        },
        legend: {
          data: [
            "电源电压",
            "管道温度",
            "照度",
            "运行模式",
            "虫仓号",
            "错误码",
            "当前电机",
            "电机方向",
            "经度",
            "纬度",
            "室外温度",
            "进入低温休眠",
            "低温休眠开关",
            "加热",
            "诱虫",
            "补光",
            "屏幕电源",
            "振动",
            "上虫仓",
            "下虫仓",
            "传送带",
          ],
          textStyle: {
            color: "#fff",
          },
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true,
        },
        toolbox: {
          feature: {
            saveAsImage: {},
          },
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: dataTime,
        },
        yAxis: {
          type: "value",
        },
        series: [
          {
            name: "电源电压",
            type: "line",
            stack: "Total",
            data: obj.e1,
          },
          {
            name: "管道温度",
            type: "line",
            stack: "Total",
            data: obj.e2,
          },
          {
            name: "照度",
            type: "line",
            stack: "Total",
            data: obj.e3,
          },
          {
            name: "运行模式",
            type: "line",
            stack: "Total",
            data: obj.e4,
          },
          {
            name: "虫仓号",
            type: "line",
            stack: "Total",
            data: obj.e5,
          },
          {
            name: "错误码",
            type: "line",
            stack: "Total",
            data: obj.e6,
          },
          {
            name: "当前电机",
            type: "line",
            stack: "Total",
            data: obj.e7,
          },
          {
            name: "电机方向",
            type: "line",
            stack: "Total",
            data: obj.e8,
          },
          {
            name: "经度",
            type: "line",
            stack: "Total",
            data: obj.e9,
          },
          {
            name: "纬度",
            type: "line",
            stack: "Total",
            data: obj.e10,
          },
          {
            name: "室外温度",
            type: "line",
            stack: "Total",
            data: obj.e13,
          },
          {
            name: "进入低温休眠",
            type: "line",
            stack: "Total",
            data: obj.e14,
          },
          {
            name: "加热",
            type: "line",
            stack: "Total",
            data: obj.e15,
          },
          {
            name: "诱虫",
            type: "line",
            stack: "Total",
            data: obj.e16,
          },
          {
            name: "补光",
            type: "line",
            stack: "Total",
            data: obj.e17,
          },
          {
            name: "屏幕电源",
            type: "line",
            stack: "Total",
            data: obj.e18,
          },
          {
            name: "振动",
            type: "line",
            stack: "Total",
            data: obj.e19,
          },
          {
            name: "上虫仓",
            type: "line",
            stack: "Total",
            data: obj.e20,
          },
          {
            name: "下虫仓",
            type: "line",
            stack: "Total",
            data: obj.e21,
          },
          {
            name: "传送带",
            type: "line",
            stack: "Total",
            data: obj.e22,
          },
        ],
      };
      option && myChart.setOption(option);
    },
    rowClass() {
      return "text-align:center";
    },
    init() {
      axios
        .post("http://115.28.187.9:8005/login", {
          username: "527050164",
          password: "123456",
        })
        .then((response) => {
          this.token = response.data.token;
          this.getRealInfo();
          this.getTableInfo();
        });
    },
    getSweather() {
      axios({
        method: "get",
        url: "https://v0.yiketianqi.com/api?unescape=1&version=v9&appid=57187519&appsecret=Demz91pJ",
      }).then((res) => {
        this.weatherList = res.data.data;
      });
    },
    getRealInfo() {
      axios({
        method: "get",
        url: "http://115.28.187.9:8005/data/16086393",
        headers: { token: this.token },
      }).then((res) => {
        this.realInfo = res.data;
      });
    },
    getTableInfo() {
      axios({
        method: "get",
        url: "http://115.28.187.9:8005/datas/16086393?interval=1&pageNum=1&pageSize=20&sort=DESC",
        headers: { token: this.token },
      }).then((res) => {
        this.tableData = res.data;
        for (let i = 0; i < this.tableData.length; i++) {
          this.tableData[i].e1 = this.tableData[i].e1 / 10;
          this.tableData[i].e3 = this.tableData[i].e3 / 10;
          this.tableData[i].e5 = this.tableData[i].e5 / 10;
          this.tableData[i].e8 = this.tableData[i].e8 / 100;
          this.tableData[i].e9 = this.tableData[i].e9 / 10;
          this.tableData[i].e10 = this.tableData[i].e10 * 10;
          this.tableData[i].e11 = this.tableData[i].e11 / 10;
          this.tableData[i].e12 = this.tableData[i].e12 / 10;
          this.tableData[i].e13 = this.tableData[i].e13 / 10;
          this.tableData[i].e14 = this.tableData[i].e14 / 10;
          this.tableData[i].e15 = this.tableData[i].e15 / 10;
          this.tableData[i].e16 = this.tableData[i].e16 / 10;
          this.tableData[i].e17 = this.tableData[i].e17 / 10;
          this.tableData[i].e18 = this.tableData[i].e18 / 10;
        }
        let dateTime = res.data.map((v) => v.dataTime);
        let obj = {};
        obj.e1 = res.data.map((v) => v.e1);
        obj.e2 = res.data.map((v) => v.e2);
        obj.e3 = res.data.map((v) => v.e3);
        obj.e4 = res.data.map((v) => v.e4);
        obj.e5 = res.data.map((v) => v.e5);
        obj.e6 = res.data.map((v) => v.e6);
        obj.e7 = res.data.map((v) => v.e7);
        obj.e8 = res.data.map((v) => v.e8);
        obj.e9 = res.data.map((v) => v.e9);
        obj.e10 = res.data.map((v) => v.e10);
        obj.e11 = res.data.map((v) => v.e11);
        obj.e12 = res.data.map((v) => v.e12);
        obj.e13 = res.data.map((v) => v.e13);
        obj.e14 = res.data.map((v) => v.e14);
        obj.e15 = res.data.map((v) => v.e15);
        obj.e16 = res.data.map((v) => v.e16);
        obj.e17 = res.data.map((v) => v.e17);
        obj.e18 = res.data.map((v) => v.e18);
        this.draw(dateTime, obj);
      });
    },
    initInsect() {
      this.getInsectInfo();
      this.getTableInfo2();
      this.getPicList();
    },
    getInsectInfo() {
      axios({
        method: "get",
        url: "http://115.28.187.9:8005/pest/dataextend/864819057844282",
        headers: { token: this.token },
      }).then((res) => {
        this.insectInfo = res.data;
      });
    },
    getTableInfo2() {
      axios({
        method: "get",
        url: "http://115.28.187.9:8005/pest/dataextends/864819057844282?pageNum=1&pageSize=20&sort=DESC",
        headers: { token: this.token },
      }).then((res) => {
        this.tableData2 = res.data;
        let dateTime = res.data.map((v) => v.dataTime);
        let obj = {};
        for (let i = 0; i < this.tableData2.length; i++) {
          this.tableData2[i].e1 = this.tableData2[i].e1 / 1000;
          this.tableData2[i].e2 = this.tableData2[i].e2 / 10;
          this.tableData2[i].e3 = this.tableData2[i].e3 / 1000;
          this.tableData2[i].e9 = this.tableData2[i].e9 / 10;
          this.tableData2[i].e10 = this.tableData2[i].e10 * 10;
          this.tableData2[i].e13 = this.tableData2[i].e13 / 10;
          this.tableData2[i].e14 = this.tableData2[i].e14 / 10;
          this.tableData2[i].e15 = this.tableData2[i].e15 / 10;
          this.tableData2[i].e16 = this.tableData2[i].e16 / 10;
          this.tableData2[i].e17 = this.tableData2[i].e17 / 10;
          this.tableData2[i].e18 = this.tableData2[i].e18 / 10;
        }
        obj.e1 = res.data.map((v) => v.e1);
        obj.e2 = res.data.map((v) => v.e2);
        obj.e3 = res.data.map((v) => v.e3);
        obj.e4 = res.data.map((v) => v.e4);
        obj.e5 = res.data.map((v) => v.e5);
        obj.e6 = res.data.map((v) => v.e6);
        obj.e7 = res.data.map((v) => v.e7);
        obj.e8 = res.data.map((v) => v.e8);
        obj.e9 = res.data.map((v) => v.e9);
        obj.e10 = res.data.map((v) => v.e10);
        obj.e13 = res.data.map((v) => v.e13);
        obj.e14 = res.data.map((v) => v.e14);
        obj.e15 = res.data.map((v) => v.e15);
        obj.e16 = res.data.map((v) => v.e16);
        obj.e17 = res.data.map((v) => v.e17);
        obj.e18 = res.data.map((v) => v.e18);
        obj.e19 = res.data.map((v) => v.e19);
        obj.e20 = res.data.map((v) => v.e20);
        obj.e21 = res.data.map((v) => v.e21);
        obj.e22 = res.data.map((v) => v.e22);
        obj.e23 = res.data.map((v) => v.e23);
        // this.draw2(dateTime, obj);
      });
    },
    getPicList() {
      axios({
        url: "http://115.28.187.9:8005/pest/images/864819057844282?pageNum=1&pageSize=6&sort=DESC",
        headers: { token: this.token },
        method: "get",
      }).then((res) => {
        this.picList = res.data;
        for (let i = 0; i < this.picList.length; i++) {
          this.picList[i].result = JSON.parse(this.picList[i].result);
        }
      });
    },
  },
  mounted() {
    this.init();
    this.getSweather();
  },
};
</script>

<style scoped>
::v-deep .el-table {
  background-color: transparent;
  color: #fff;
}
::v-deep .el-table__body-wrapper::-webkit-scrollbar {
  width: 6px;
  height: 14px;
}
::v-deep .el-table__fixed {
  height: auto !important;
  bottom: 18px;
}
::v-deep .el-table__fixed-right {
  height: auto !important;
  bottom: 18px;
}

::v-deep .el-table__body-wrapper::-webkit-scrollbar-thumb {
  background-color: red;
  border-radius: 3px;
  z-index: 99;
}
::v-deep .el-table tr {
  background-color: transparent;
}
::v-deep .el-table th.el-table__cell {
  background-color: transparent;
}

::v-deep .el-table__body tr.hover-row > td.el-table__cell {
  background-color: rgb(65, 65, 179) !important;
}
.container {
  width: 100%;
}
.container header {
  text-align: center;
  margin: 20px 0;
  line-height: 1.15;
  position: relative;
}
.container header .sweather {
  position: absolute;
  display: flex;
  align-items: center;
  bottom: -1.875rem;
}
.container header .sweather .sweather-item {
  color: #fff;
  padding: 0 0.9375rem;
}
.container header .time {
  position: absolute;
  right: 1.25rem;
  bottom: 0.4375rem;
  color: #acb1bc;
}
.container main {
  display: grid;
  grid-auto-flow: column;
  grid-template-rows: repeat(2, 28rem);
}
.container main .stations {
  display: flex;
  width: 98vw;
}
.container main .stations-select {
  flex-basis: 6.85rem;
  flex-shrink: 0;
  padding: 0.625rem;
}
.container main .stations-select li {
  padding: 0.425rem;
}
.container main .stations-select .selected {
  background-color: #999;
}
.container main .stations .section {
  display: flex;
  justify-content: space-around;
  flex-grow: 1;
  width: 80%;
}
.container main .stations .section-item {
}
.container main .stations .section-item h3 {
  padding: 0.3125rem 0.925rem;
  margin-left: 0.0125rem;
  position: relative;
}
.container main .stations .section-item h3::after {
  content: "";
  display: block;
  width: 5px;
  height: 20px;
  background-color: rgb(0, 183, 255);
  position: absolute;
  top: 7px;
  left: 5px;
}
.container main .stations .section-item .table {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  margin-left: 0.625rem;
  margin-top: 2.1875rem;
}
.container main .stations .section-item .table-item {
  display: flex;
  flex-basis: 31%;
  flex-grow: 0;
  flex-shrink: 0;
  padding: 1.0125rem 0.125rem;
  border: 1px solid #3285b9;
  font-size: 0.875rem;
}
.container main .stations .section-item .table-item-title {
  width: 4.5rem;
  color: #fff;
}
.container main .stations .section-item .table-item-value {
  color: yellow;
  padding-left: 0.125rem;
}
.container main .stations .section1 {
  display: flex;
  flex-grow: 1;
}
.container main .stations .section1-item {
  flex: 0 0 16.6%;
}
.container main .stations .section1-item h3 {
  padding: 0.8125rem;
  text-align: center;
}
.container main .stations .section1-item .image {
  height: 20rem;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.container main .stations .section1-item .image img {
  height:auto;
  width: 96%;
}
.container main .analysis {
  margin-top: 2.675rem;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}
.container main .analysis .analysis-first {
  display: flex;
  justify-content: center;
  align-items: center;
  align-self: flex-start;
  color: #fff;
  flex-basis: 6.85rem;
  flex-shrink: 0;
  background-color: #132e78;
}
.container main .analysis-item h3 {
  padding: 0.625rem 0.9375rem;
  position: relative;
}
.container main .analysis-item h3::after {
  content: "";
  display: block;
  width: 5px;
  height: 20px;
  background-color: rgb(240, 18, 111);
  position: absolute;
  top: 12px;
  left: 5px;
}
.container main .analysis-item p {
  color: #fff;
  padding: 0.625rem;
}

.container main .analysis-item ol li {
  padding: 0.9375rem;
}
.container main .analysis-item {
  padding: 0.9375rem;
}
.pic {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  margin-top: 2.5rem;
}
.pic .pic-item {
  flex: 0 0 28%;
  margin: 10px;
}
.pic .pic-item .pic-item-info {
  color: rgb(28, 138, 234);
  text-align: center;
  font-size: 12px;
}
</style>
