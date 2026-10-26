<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>GLB 上色 / 材质编辑器</title>
<style>
  * { box-sizing: border-box; }
  html, body {
    margin: 0; height: 100%; overflow: hidden; background: #15161a;
    font-family: system-ui, -apple-system, "Segoe UI", sans-serif; color: #e8e8ee;
  }
  #canvas { display: block; width: 100%; height: 100%; touch-action: none; }
  .bar { position: fixed; z-index: 10; }
  #topbar {
    top: 0; left: 0; right: 0; display: flex; gap: 8px; align-items: center;
    padding: 10px 14px; flex-wrap: wrap;
    background: linear-gradient(to bottom, rgba(21,22,26,.92), rgba(21,22,26,0));
  }
  button {
    font: inherit; border: 0; border-radius: 8px; padding: 8px 14px;
    cursor: pointer; background: #2a2d36; color: #e8e8ee; transition: background .15s;
  }
  button:hover { background: #373b47; }
  button.primary { background: #4f8cff; color: #fff; }
  button.primary:hover { background: #3a74e0; }
  button:disabled { opacity: .4; cursor: default; }
  #panel {
    right: 14px; bottom: 14px; width: 268px; padding: 14px;
    border-radius: 14px; background: rgba(30,32,38,.94);
    backdrop-filter: blur(10px); box-shadow: 0 8px 30px rgba(0,0,0,.45);
  }
  #panel h3 { margin: 0 0 10px; font-size: 13px; font-weight: 600; opacity: .7; }
  .row { display: flex; align-items: center; gap: 8px; margin-bottom: 10px; }
  .row label { font-size: 12px; opacity: .7; width: 52px; flex: none; }
  input[type="color"] {
    width: 100%; height: 34px; border: 0; border-radius: 8px;
    background: none; padding: 0; cursor: pointer;
  }
  input[type="range"] { flex: 1; accent-color: #4f8cff; }
  .value { width: 38px; text-align: right; font-size: 12px; opacity: .7; }
  .presets { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; margin-bottom: 10px; }
  .presets button { padding: 7px 6px; font-size: 12px; }
  .hint { font-size: 11px; opacity: .45; line-height: 1.5; margin-top: 10px; }
  #empty {
    position: fixed; inset: 0; display: flex; flex-direction: column;
    align-items: center; justify-content: center; text-align: center;
    color: #888; pointer-events: none; gap: 6px; padding: 24px;
  }
  #empty h1 { color: #fff; font-size: 18px; margin: 0; }
  #empty p { margin: 0; font-size: 13px; }
  #drop {
    position: fixed; inset: 0; display: none; align-items: center; justify-content: center;
    z-index: 30; background: rgba(79,140,255,.2); border: 3px dashed #4f8cff;
    color: #fff; font-size: 20px;
  }
  #drop.show { display: flex; }
  #selname { font-size: 12px; opacity: .6; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; max-width: 45vw; }
  .disabled { opacity: .4; pointer-events: none; }
  @media (max-width: 560px) {
    #panel { right: 10px; left: 10px; bottom: 10px; width: auto; }
  }
</style>
</head>
<body>
<canvas id="canvas"></canvas>

<div id="topbar" class="bar">
  <button class="primary" id="pickBtn">打开 GLB</button>
  <input type="file" id="file" accept=".glb,.gltf,model/gltf-binary" hidden />
  <button id="exportBtn" disabled>导出 GLB</button>
  <span id="selname">未选中对象</span>
</div>

<div id="panel" class="bar disabled">
  <h3>材质</h3>
  <div class="row">
    <label>颜色</label>
    <input type="color" id="color" value="#cccccc" />
  </div>
  <div class="presets">
    <button data-preset="stainless">不锈钢</button>
    <button data-preset="aluminum">铝</button>
    <button data-preset="polished">镜面</button>
    <button data-preset="matte">哑光金属</button>
    <button data-preset="plastic">塑料</button>
    <button data-preset="rubber">橡胶</button>
  </div>
  <div class="row">
    <label>金属度</label>
    <input type="range" id="metalness" min="0" max="1" step="0.01" value="0" />
    <span class="value" id="metalnessVal">0.00</span>
  </div>
  <div class="row">
    <label>粗糙度</label>
    <input type="range" id="roughness" min="0" max="1" step="0.01" value="0.5" />
    <span class="value" id="roughnessVal">0.50</span>
  </div>
  <div class="row" style="margin-bottom:0">
    <button style="flex:1" id="applyAll">应用到全部</button>
    <button style="flex:1" id="resetSel">恢复</button>
  </div>
  <div class="hint">金属材质需要环境反射，在支持 IBL 的查看器里显示才正确。</div>
</div>

<div id="empty">
  <h1>拖入 .glb 文件，或点击“打开 GLB”</h1>
  <p>点击模型部位选中，再修改颜色和材质</p>
</div>

<div id="drop">松开鼠标加载模型</div>

<script type="importmap">
{
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/"
  }
}
</script>

<script type="module">
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
import { GLTFExporter } from 'three/addons/exporters/GLTFExporter.js';
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js';
import { MeshoptDecoder } from 'three/addons/libs/meshopt_decoder.module.js';
import { RoomEnvironment } from 'three/addons/environments/RoomEnvironment.js';

/* ---------- 基础场景 ---------- */
const canvas = document.getElementById('canvas');
const renderer = new THREE.WebGLRenderer({ canvas, antialias: true });
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
renderer.outputColorSpace = THREE.SRGBColorSpace;
renderer.toneMapping = THREE.ACESFilmicToneMapping;
renderer.toneMappingExposure = 1.0;

const scene = new THREE.Scene();
scene.background = new THREE.Color(0x1b1d23);

const camera = new THREE.PerspectiveCamera(45, 1, 0.01, 1000);
camera.position.set(2, 1.5, 3);

const controls = new OrbitControls(camera, canvas);
controls.enableDamping = true;
controls.dampingFactor = 0.08;

// 环境反射：金属材质必须要有，否则会发黑
const pmrem = new THREE.PMREMGenerator(renderer);
const roomEnv = new RoomEnvironment();
scene.environment = pmrem.fromScene(roomEnv, 0.04).texture;
roomEnv.dispose?.();
pmrem.dispose();

function resize() {
  const w = window.innerWidth, h = window.innerHeight;
  renderer.setSize(w, h, false);
  camera.aspect = w / h;
  camera.updateProjectionMatrix();
}
window.addEventListener('resize', resize);
resize();

renderer.setAnimationLoop(() => {
  controls.update();
  boxHelper?.update();
  renderer.render(scene, camera);
});

/* ---------- 加载器 ---------- */
const loader = new GLTFLoader();
const dracoLoader = new DRACOLoader();
dracoLoader.setDecoderPath('https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/libs/draco/');
loader.setDRACOLoader(dracoLoader);
loader.setMeshoptDecoder(MeshoptDecoder);

/* ---------- 状态 ---------- */
let modelRoot = null;
let selectedMesh = null;
let boxHelper = null;
let baseName = 'model';
const originalMaterials = new WeakMap(); // mesh -> 原始材质

/* ---------- 加载 / 清空 ---------- */
function loadFile(file) {
  if (!file) return;
  if (!/\.(glb|gltf)$/i.test(file.name)) {
    alert('请选择 .glb 或 .gltf 文件');
    return;
  }
  baseName = file.name.replace(/\.(glb|gltf)$/i, '');
  const url = URL.createObjectURL(file);
  loader.load(url, (gltf) => {
    URL.revokeObjectURL(url);
    setModel(gltf.scene);
  }, undefined, (err) => {
    URL.revokeObjectURL(url);
    console.error(err);
    alert('加载失败，请确认是有效的 GLB 文件');
  });
}

function setModel(root) {
  clearModel();
  modelRoot = root;
  scene.add(root);
  fitView(root);
  document.getElementById('empty').style.display = 'none';
  document.getElementById('exportBtn').disabled = false;
}

function clearModel() {
  if (modelRoot) {
    scene.remove(modelRoot);
    modelRoot.traverse((o) => {
      if (!o.isMesh) return;
      o.geometry?.dispose?.();
      const mats = Array.isArray(o.material) ? o.material : [o.material];
      mats.forEach((m) => m?.dispose?.());
    });
  }
  modelRoot = null;
  select(null);
}

function fitView(root) {
  const box = new THREE.Box3().setFromObject(root);
  const size = box.getSize(new THREE.Vector3());
  const center = box.getCenter(new THREE.Vector3());
  const maxDim = Math.max(size.x, size.y, size.z) || 1;
  const dist = (maxDim / (2 * Math.tan((camera.fov * Math.PI) / 360))) * 1.6;

  const dir = new THREE.Vector3(1, 0.8, 1).normalize();
  camera.position.copy(center).addScaledVector(dir, dist);
  camera.near = maxDim / 1000;
  camera.far = maxDim * 100;
  camera.updateProjectionMatrix();
  controls.target.copy(center);
  controls.update();
}

/* ---------- 选中 ---------- */
const raycaster = new THREE.Raycaster();
const pointer = new THREE.Vector2();
let downPos = null;

canvas.addEventListener('pointerdown', (e) => {
  downPos = { x: e.clientX, y: e.clientY };
});

canvas.addEventListener('pointerup', (e) => {
  if (!downPos || !modelRoot) { downPos = null; return; }
  const dx = e.clientX - downPos.x;
  const dy = e.clientY - downPos.y;
  downPos = null;
  if (dx * dx + dy * dy > 25) return; // 拖动不算点击

  const rect = canvas.getBoundingClientRect();
  pointer.x = ((e.clientX - rect.left) / rect.width) * 2 - 1;
  pointer.y = -((e.clientY - rect.top) / rect.height) * 2 + 1;
  raycaster.setFromCamera(pointer, camera);

  const hits = raycaster.intersectObject(modelRoot, true)
    .filter((h) => h.object.isMesh && h.object.visible);

  select(hits.length ? hits[0].object : null);
});

function select(mesh) {
  selectedMesh = mesh;

  if (boxHelper) {
    scene.remove(boxHelper);
    boxHelper.geometry.dispose();
    boxHelper.material.dispose();
    boxHelper = null;
  }

  const panel = document.getElementById('panel');
  const selname = document.getElementById('selname');

  if (mesh) {
    boxHelper = new THREE.BoxHelper(mesh, 0x4f8cff);
    scene.add(boxHelper);
    panel.classList.remove('disabled');
    selname.textContent = mesh.name || '未命名部件';
    syncPanel(mesh);
  } else {
    panel.classList.add('disabled');
    selname.textContent = '未选中对象';
  }
}

function firstMaterial(mesh) {
  if (!mesh) return null;
  return Array.isArray(mesh.material) ? mesh.material[0] : mesh.material;
}

/* ---------- 材质编辑 ---------- */
function ensureEditable(mesh) {
  if (!originalMaterials.has(mesh)) {
    originalMaterials.set(
      mesh,
      Array.isArray(mesh.material) ? [...mesh.material] : mesh.material
    );
  }

  const clone = (m) => {
    if (!m) return new THREE.MeshStandardMaterial();
    if (m.isMeshStandardMaterial) {
      if (m.userData.__cloned) return m;
      const c = m.clone();
      c.userData.__cloned = true;
      return c;
    }
    const c = new THREE.MeshStandardMaterial({
      color: m.color ? m.color.clone() : new THREE.Color(0xffffff),
      map: m.map || null,
      metalness: 0,
      roughness: 0.8,
      transparent: m.transparent,
      opacity: m.opacity,
      side: m.side,
    });
    c.userData.__cloned = true;
    return c;
  };

  if (Array.isArray(mesh.material)) {
    mesh.material = mesh.material.map(clone);
  } else {
    mesh.material = clone(mesh.material);
  }
}

function setProps(mesh, props) {
  ensureEditable(mesh);
  const mats = Array.isArray(mesh.material) ? mesh.material : [mesh.material];
  for (const m of mats) {
    if (!m) continue;
    if (props.color !== undefined && m.color) m.color.set(props.color);
    if (props.metalness !== undefined && 'metalness' in m) m.metalness = props.metalness;
    if (props.roughness !== undefined && 'roughness' in m) m.roughness = props.roughness;
    m.needsUpdate = true;
  }
}

function setPropsAll(props) {
  if (!modelRoot) return;
  modelRoot.traverse((o) => { if (o.isMesh) setProps(o, props); });
}

function resetSelected() {
  if (!selectedMesh) return;
  const orig = originalMaterials.get(selectedMesh);
  if (orig) {
    const mats = Array.isArray(selectedMesh.material) ? selectedMesh.material : [selectedMesh.material];
    mats.forEach((m) => { if (m?.userData.__cloned) m.dispose(); });
    selectedMesh.material = Array.isArray(orig) ? [...orig] : orig;
    originalMaterials.delete(selectedMesh);
  }
  syncPanel(selectedMesh);
}

/* ---------- UI ---------- */
const colorInput = document.getElementById('color');
const metalnessInput = document.getElementById('metalness');
const roughnessInput = document.getElementById('roughness');
const metalnessVal = document.getElementById('metalnessVal');
const roughnessVal = document.getElementById('roughnessVal');

const PRESETS = {
  stainless: { color: '#e8e8e8', metalness: 1, roughness: 0.18 },
  aluminum:  { color: '#d8dadd', metalness: 1, roughness: 0.38 },
  polished:  { color: '#f2f2f2', metalness: 1, roughness: 0.05 },
  matte:     { color: '#b8bcc2', metalness: 0.9, roughness: 0.6 },
  plastic:   { color: '#4f8cff', metalness: 0, roughness: 0.45 },
  rubber:    { color: '#2a2a2a', metalness: 0, roughness: 0.95 },
};

function syncPanel(mesh) {
  const m = firstMaterial(mesh);
  if (!m) return;
  if (m.color) colorInput.value = '#' + m.color.getHexString();
  const metal = 'metalness' in m ? m.metalness : 0;
  const rough = 'roughness' in m ? m.roughness : 0.5;
  metalnessInput.value = metal;
  roughnessInput.value = rough;
  metalnessVal.textContent = Number(metal).toFixed(2);
  roughnessVal.textContent = Number(rough).toFixed(2);
}

colorInput.addEventListener('input', () => {
  if (!selectedMesh) return;
  setProps(selectedMesh, { color: colorInput.value });
});

metalnessInput.addEventListener('input', () => {
  metalnessVal.textContent = Number(metalnessInput.value).toFixed(2);
  if (!selectedMesh) return;
  setProps(selectedMesh, { metalness: Number(metalnessInput.value) });
});

roughnessInput.addEventListener('input', () => {
  roughnessVal.textContent = Number(roughnessInput.value).toFixed(2);
  if (!selectedMesh) return;
  setProps(selectedMesh, { roughness: Number(roughnessInput.value) });
});

document.querySelectorAll('[data-preset]').forEach((btn) => {
  btn.addEventListener('click', () => {
    if (!selectedMesh) return;
    const p = PRESETS[btn.dataset.preset];
    setProps(selectedMesh, p);
    syncPanel(selectedMesh);
  });
});

document.getElementById('applyAll').addEventListener('click', () => {
  setPropsAll({
    color: colorInput.value,
    metalness: Number(metalnessInput.value),
    roughness: Number(roughnessInput.value),
  });
});

document.getElementById('resetSel').addEventListener('click', resetSelected);

/* ---------- 文件选择 / 拖放 ---------- */
const fileInput = document.getElementById('file');
document.getElementById('pickBtn').addEventListener('click', () => fileInput.click());
fileInput.addEventListener('change', () => loadFile(fileInput.files[0]));

const dropEl = document.getElementById('drop');
let dragCount = 0;

window.addEventListener('dragenter', (e) => {
  e.preventDefault();
  dragCount++;
  dropEl.classList.add('show');
});
window.addEventListener('dragover', (e) => e.preventDefault());
window.addEventListener('dragleave', (e) => {
  e.preventDefault();
  dragCount--;
  if (dragCount <= 0) { dragCount = 0; dropEl.classList.remove('show'); }
});
window.addEventListener('drop', (e) => {
  e.preventDefault();
  dragCount = 0;
  dropEl.classList.remove('show');
  const f = e.dataTransfer.files[0];
  if (f) loadFile(f);
});

/* ---------- 导出 ---------- */
document.getElementById('exportBtn').addEventListener('click', () => {
  if (!modelRoot) return;
  const btn = document.getElementById('exportBtn');
  const oldText = btn.textContent;
  btn.disabled = true;
  btn.textContent = '导出中…';

  if (boxHelper) boxHelper.visible = false;

  const exporter = new GLTFExporter();
  exporter.parse(
    modelRoot,
    (result) => {
      const blob = new Blob([result], { type: 'model/gltf-binary' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = baseName + '-edited.glb';
      document.body.appendChild(a);
      a.click();
      a.remove();
      setTimeout(() => URL.revokeObjectURL(url), 1000);

      if (boxHelper) boxHelper.visible = true;
      btn.disabled = false;
      btn.textContent = oldText;
    },
    (err) => {
      console.error(err);
      alert('导出失败：' + (err?.message || err));
      if (boxHelper) boxHelper.visible = true;
      btn.disabled = false;
      btn.textContent = oldText;
    },
    { binary: true }
  );
});
</script>
</body>
</html>
