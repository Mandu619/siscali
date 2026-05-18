let funcionarios=[]; let editIdx=null; let flujo={estado:'Sin planilla importada', historial:[]}; let archivoInfo={nombre:'', hojas:[], fecha:''}; let planillaActualId=null; let reviewSearch=''; let datosProcesoAsignados=false;
let currentUser=null;
const defaultUsers=[{nombre:'Administrador General',email:'admin@sistema.cl',pass:'admin123',role:'Administrador General'}];
function getPlanillas(){try{return JSON.parse(localStorage.getItem('ta_planillas'))||[]}catch(e){return []}}
function savePlanillas(arr){localStorage.setItem('ta_planillas',JSON.stringify(arr))}

function getFinanzas(){try{return JSON.parse(localStorage.getItem('ta_finanzas'))||{montoBase:0,bloqueado:false,movs:[]}}catch(e){return {montoBase:0,bloqueado:false,movs:[]}}}
function saveFinanzas(f){localStorage.setItem('ta_finanzas',JSON.stringify(f))}
function saldoFinancieroBase(fin=getFinanzas()){return (Number(fin.montoBase)||0)+(fin.movs||[]).filter(m=>m.tipo!=='Definición inicial').reduce((a,m)=>a+(Number(m.monto)||0),0)}
function totalPlanillasAprobadas(){return getPlanillas().filter(x=>!x.eliminada&&(x.flujo?.estado||'')==='Aprobado para carga').reduce((a,x)=>a+(Number(x.total)||0),0)}
function saldoFinanzas(){return saldoFinancieroBase()-totalPlanillasAprobadas()}
function aceptarMontoFinanzas(){
 if(!canWorkAsAnalyst()){alert('Solo el Analista puede administrar finanzas.');return}
 const f=getFinanzas();
 if(f.bloqueado){alert('El monto ya está aceptado y bloqueado. Para cambiarlo use “Modificar monto con justificación”.');return}
 const val=num(finMontoInput.value);
 if(val<=0){alert('Debe ingresar un monto total disponible mayor a cero.');finMontoInput.focus();return}
 f.montoBase=val; f.bloqueado=true; f.movs=f.movs||[];
 f.movs.unshift({fecha:new Date().toLocaleString('es-CL'),tipo:'Definición inicial',monto:val,justificacion:'Monto total disponible aceptado y bloqueado por el analista.',usuario:currentUser?.email||''});
 saveFinanzas(f); render(); toastMsg('Monto financiero aceptado y bloqueado.');
}
function modificarMontoFinanzas(){
 if(!canWorkAsAnalyst()){alert('Solo el Analista puede administrar finanzas.');return}
 const f=getFinanzas();
 if(!f.bloqueado){alert('Primero debe aceptar y bloquear un monto inicial.');return}
 const nuevo=prompt('Indique el nuevo monto total disponible o un ajuste con signo (+/-). Ej: 120000000 o +250000 o -100000');
 if(nuevo===null)return;
 const txt=String(nuevo).trim(); if(!txt){alert('Debe ingresar un monto.');return}
 const just=prompt('Justifique la modificación. Ej: licitación nueva, reintegro, reversa o egreso durante el mes.');
 if(just===null)return;
 if(!String(just).trim()){alert('La justificación es obligatoria.');return}
 let monto=0, tipo='Modificación de monto disponible';
 if(txt.startsWith('+')||txt.startsWith('-')){monto=num(txt); tipo=monto>=0?'Reintegro / aumento disponible':'Egreso / disminución disponible';}
 else {const nuevoTotal=num(txt); monto=nuevoTotal-saldoFinancieroBase(f); tipo='Nuevo monto total disponible';}
 if(!monto){alert('El monto ingresado no genera cambios.');return}
 f.movs=f.movs||[]; f.movs.unshift({fecha:new Date().toLocaleString('es-CL'),tipo,monto,justificacion:String(just).trim(),usuario:currentUser?.email||''});
 saveFinanzas(f); render(); toastMsg('Monto financiero modificado con justificación.');
}
function renderFinanzas(){
 const f=getFinanzas(); const base=saldoFinancieroBase(f); const usado=totalPlanillasAprobadas(); const saldo=base-usado;
 if(document.getElementById('anioAutoVista')) anioAutoVista.value=new Date().getFullYear();
 if(document.getElementById('finMontoInput')){finMontoInput.value=f.bloqueado?base:(f.montoBase||''); finMontoInput.disabled=!!f.bloqueado;}
 if(document.getElementById('finBloqueoEstado')) finBloqueoEstado.value=f.bloqueado?'Aceptado y bloqueado':'Pendiente de aceptación';
 if(document.getElementById('finUsadoInput')) finUsadoInput.value=money(usado);
 if(document.getElementById('finSaldoInput')) finSaldoInput.value=money(saldo);
 if(document.getElementById('finInicial')) finInicial.textContent=money(base);
 if(document.getElementById('finUsado')) finUsado.textContent=money(usado);
 if(document.getElementById('finSaldo')) finSaldo.textContent=money(saldo);
 if(document.getElementById('finEstado')) finEstado.textContent=f.bloqueado?'Monto financiero bloqueado con control de modificaciones':'Monto financiero pendiente de aceptación';
 if(document.getElementById('tbodyFinanzasMov')) tbodyFinanzasMov.innerHTML=(f.movs||[]).length?(f.movs||[]).map(m=>`<tr><td>${m.fecha||''}</td><td>${m.tipo||''}</td><td><b>${money(m.monto)}</b></td><td>${m.justificacion||''}</td><td>${m.usuario||''}</td></tr>`).join(''):'<tr><td colspan="5">Sin movimientos financieros registrados.</td></tr>';
 const aprobadas=getPlanillas().filter(x=>!x.eliminada&&(x.flujo?.estado||'')==='Aprobado para carga');
 if(document.getElementById('tbodyFinanzasPlanillas')) tbodyFinanzasPlanillas.innerHTML=aprobadas.length?aprobadas.map(x=>`<tr><td><b>${x.nombre||'Sin identificador'}</b><br><span class="small">${x.archivoInfo?.nombre||''}</span></td><td>${etapaHTML(x.flujo?.estado)}</td><td><b>${money(x.total||0)}</b></td></tr>`).join(''):'<tr><td colspan="3">No existen planillas aprobadas para descontar del saldo.</td></tr>';
 renderEdenredModule();
}
function snapshotPlanilla(){
 const all=funcionarios.map(computed); const total=all.reduce((a,f)=>a+f.total,0); const p=params();
 return {id:planillaActualId||('pl_'+Date.now()), nombre:(planillaNombre?.value||'').trim(), mes:p.mes, anio:p.anio, inicial:p.inicial, obs:obsGeneral?.value||'', datosProcesoAsignados, archivoInfo, funcionarios, flujo, total, cantidad:funcionarios.length, actualizado:new Date().toLocaleString('es-CL'), analista:currentUser?.email||''};
}
function guardarPlanillaActual(){ if(!planillaActualId) return; const snap=snapshotPlanilla(); const arr=getPlanillas(); const ix=arr.findIndex(x=>x.id===snap.id); if(ix>=0) arr[ix]=snap; else arr.unshift(snap); savePlanillas(arr); }
function cargarPlanilla(id){ const pl=getPlanillas().find(x=>x.id===id); if(!pl){alert('No se encontró la planilla seleccionada.');return} planillaActualId=pl.id; funcionarios=pl.funcionarios||[]; flujo=pl.flujo||{estado:'Sin planilla importada',historial:[]}; archivoInfo=pl.archivoInfo||{nombre:'',hojas:[],fecha:''}; if(document.getElementById('mes')) mes.value=pl.mes||''; if(document.getElementById('anio')) anio.value=pl.anio||new Date().getFullYear(); if(document.getElementById('montoInicial')) montoInicial.value=pl.inicial||0; if(document.getElementById('obsGeneral')) obsGeneral.value=pl.obs||''; if(document.getElementById('planillaNombre')) planillaNombre.value=pl.nombre||''; datosProcesoAsignados=!!pl.datosProcesoAsignados; render(); }
function planillasParaRol(){ const arr=getPlanillas(); if(isJefeDepto()) return arr.filter(x=>x.eliminada||['Enviado a validación técnica','Validado técnicamente','Devuelto a analista','Aprobado para carga','Rechazado por jefatura'].includes(x.flujo?.estado)); if(isJefeDivision()) return arr.filter(x=>x.eliminada||['Validado técnicamente','Aprobado para carga','Rechazado por jefatura'].includes(x.flujo?.estado)); return arr; }

function getUsers(){try{return JSON.parse(localStorage.getItem('ta_users'))||defaultUsers}catch(e){return defaultUsers}}
function saveUsers(u){localStorage.setItem('ta_users',JSON.stringify(u))}
function normalizeEmail(e){return String(e||'').trim().toLowerCase()}
function role(){return String(currentUser?.role||'').trim()}
function isAdmin(){return role()==='Administrador General'}
function isAnalista(){return role()==='Analista'}
function isJefeDepto(){return role()==='Jefe Departamento'}
function isJefeDivision(){return role()==='Jefe División'}
function canManageUsers(){return isAdmin()}
function canWorkAsAnalyst(){return isAnalista()}
function canViewOnly(){return isJefeDepto()||isJefeDivision()}
function syncPerfil(){if(document.getElementById('perfil'))perfil.value=role()||'Analista'; if(usuarioActualTxt)usuarioActualTxt.textContent=currentUser?currentUser.nombre:'Usuario'; if(rolActualTxt)rolActualTxt.textContent=currentUser?currentUser.email:''; if(rolBadge)rolBadge.textContent=role()||'Sin perfil'}
function login(){const u=getUsers().find(x=>normalizeEmail(x.email)===normalizeEmail(loginEmail.value)&&String(x.pass)===String(loginPass.value)); if(!u){alert('Correo o contraseña incorrectos.');return} currentUser={nombre:u.nombre,email:u.email,role:u.role}; sessionStorage.setItem('ta_session',JSON.stringify(currentUser)); if(['Jefe Departamento','Jefe División'].includes(currentUser.role)){planillaActualId=null; funcionarios=[]; flujo={estado:'Sin planilla importada',historial:[]}; archivoInfo={nombre:'',hojas:[],fecha:''}; reviewSearch='';} loginView.classList.add('hidden'); appMain.classList.remove('hidden'); syncPerfil(); renderUsers(); render();}
function logout(){
 // Solo se cierra la sesión activa. No se eliminan planillas, estados ni cuentas,
 // porque esos datos quedan persistidos en localStorage para mantener el seguimiento.
 sessionStorage.removeItem('ta_session');
 currentUser=null;
 planillaActualId=null; funcionarios=[]; flujo={estado:'Sin planilla importada',historial:[]}; archivoInfo={nombre:'',hojas:[],fecha:''};
 appMain.classList.add('hidden'); loginView.classList.remove('hidden');
}
function restoreSession(){const s=sessionStorage.getItem('ta_session'); if(s){try{currentUser=JSON.parse(s); loginView.classList.add('hidden'); appMain.classList.remove('hidden'); syncPerfil();}catch(e){}}}
function crearCuenta(){if(!canManageUsers()){alert('Solo el Administrador General puede crear cuentas.');return} const users=getUsers(); const email=normalizeEmail(newUserEmail.value); if(!newUserName.value.trim()||!email||!newUserPass.value){alert('Completa nombre, correo y contraseña.');return} if(newUserPass.value.length<6){alert('La contraseña temporal debe tener al menos 6 caracteres.');return} if(users.some(u=>normalizeEmail(u.email)===email)){alert('Ya existe una cuenta con ese correo.');return} users.push({nombre:newUserName.value.trim(),email,pass:newUserPass.value,role:newUserRole.value}); saveUsers(users); newUserName.value='';newUserEmail.value='';newUserPass.value=''; renderUsers(); toastMsg('Cuenta creada correctamente.');}
function eliminarCuenta(email){if(!canManageUsers())return; if(normalizeEmail(email)==='admin@sistema.cl'){alert('No se puede eliminar el administrador inicial.');return} if(confirm('¿Eliminar esta cuenta?')){saveUsers(getUsers().filter(u=>normalizeEmail(u.email)!==normalizeEmail(email)));renderUsers();}}
function renderAdminPlanillas(){
 const tbody=document.getElementById('tbodyAdminPlanillas');
 if(!tbody) return;
 if(!canManageUsers()){tbody.innerHTML=''; return;}
 const lista=getPlanillas().filter(x=>x.eliminada||(x.flujo?.estado||'')==='Aprobado para carga');
 if(!lista.length){tbody.innerHTML='<tr><td colspan="5">No hay planillas aprobadas o eliminadas para administrar.</td></tr>';return;}
 tbody.innerHTML=lista.map(x=>{
   const estado=x.eliminada?'Eliminada por administrador':(x.flujo?.estado||'');
   const accion=x.eliminada?'<span class="small">Eliminación registrada</span>':`<button class="danger mini" onclick="eliminarPlanillaAprobadaAdmin('${x.id}')">Eliminar aprobada</button>`;
   return `<tr><td><b>${x.nombre||'Sin identificador'}</b><br><span class="small">${x.archivoInfo?.nombre||''} · ${x.cantidad||0} funcionarios</span></td><td>${etapaHTML(estado)}</td><td><b>${money(x.total||0)}</b></td><td>${x.eliminacionMotivo||'-'}</td><td>${accion}</td></tr>`;
 }).join('');
}
function eliminarPlanillaAprobadaAdmin(id){
 if(!canManageUsers()){alert('Solo el Administrador General puede eliminar planillas aprobadas.');return}
 const arr=getPlanillas();
 const ix=arr.findIndex(x=>x.id===id);
 if(ix<0){alert('No se encontró la planilla.');return}
 const pl=arr[ix];
 if(pl.eliminada){alert('Esta planilla ya fue eliminada administrativamente.');return}
 if((pl.flujo?.estado||'')!=='Aprobado para carga'){alert('Solo se pueden eliminar planillas que ya estén aprobadas.');return}
 const motivo=prompt('Indique el motivo de eliminación de la planilla aprobada. Este motivo será visible para analista y jefaturas.');
 if(motivo===null)return;
 if(!String(motivo).trim()){alert('El motivo de eliminación es obligatorio.');return}
 if(!confirm('¿Confirmar eliminación administrativa de esta planilla aprobada?'))return;
 const registro={fecha:new Date().toLocaleString('es-CL'),perfil:role(),accion:'Eliminó planilla aprobada',comentario:String(motivo).trim()};
 pl.eliminada=true;
 pl.eliminacionMotivo=String(motivo).trim();
 pl.eliminadoPor=currentUser?.email||'';
 pl.eliminadoFecha=registro.fecha;
 pl.flujo=pl.flujo||{estado:'Aprobado para carga',historial:[]};
 pl.flujo.historial=pl.flujo.historial||[];
 pl.flujo.historial.unshift(registro);
 pl.flujo.estado='Eliminada por administrador';
 pl.actualizado=registro.fecha;
 arr[ix]=pl; savePlanillas(arr);
 if(planillaActualId===id){flujo=pl.flujo; funcionarios=pl.funcionarios||[];}
 render(); toastMsg('Planilla aprobada eliminada administrativamente con motivo registrado.');
}
function renderUsers(){if(!document.getElementById('tbodyUsers'))return; const users=getUsers(); tbodyUsers.innerHTML=users.map(u=>`<tr><td>${u.nombre}</td><td>${u.email}</td><td><span class="pill info">${u.role}</span></td><td>${normalizeEmail(u.email)==='admin@sistema.cl'?'-':`<button class="danger mini" onclick="eliminarCuenta('${u.email}')">Eliminar</button>`}</td></tr>`).join(''); renderAdminPlanillas();}
const descuentos=['Feriado Legal','Permisos Adm.','Descanso Complementario','Otros Permisos','Permisos sin goce','Cometidos/Comisiones','Capacitaciones','Licencias Médicas'];
const aumentos=['Horas Extraordinarias','Reintegro']; const motivos=[...descuentos,...aumentos];
const money=n=>new Intl.NumberFormat('es-CL',{style:'currency',currency:'CLP',maximumFractionDigits:0}).format(Number(n)||0);
const num=v=>{if(v===null||v===undefined||v==='')return 0; return Number(String(v).replace(',','.'))||0};
const cleanRun=r=>String(r||'').replace(/\./g,'').replace(/-/g,'').trim().toLowerCase();
const runKey=(run,dv='')=>cleanRun(String(run||'')+String(dv||''));
const fmtDate=v=>{if(!v)return ''; if(v instanceof Date)return v.toLocaleDateString('es-CL'); if(typeof v==='number'){const d=XLSX.SSF.parse_date_code(v); return d?`${String(d.d).padStart(2,'0')}-${String(d.m).padStart(2,'0')}-${d.y}`:v} return String(v)};
const toastMsg=m=>{toast.textContent=m;toast.style.display='block';setTimeout(()=>toast.style.display='none',3000)};
function cellText(v){return String(v??'').trim()}
function rowText(row){return row.map(cellText).join(' ').toLowerCase()}
function normalizeName(n){return String(n||'').normalize('NFD').replace(/[\u0300-\u036f]/g,'').toLowerCase().replace(/\s+/g,' ').trim()}
function makeGenericEvent(sheet,headers,row){const obj={tipo:sheet,campos:[]}; headers.forEach((h,i)=>{const val=row[i]; if(val!==null&&val!==undefined&&String(val).trim()!=='')obj.campos.push({campo:cellText(h)||`Columna ${i+1}`,valor:fmtDate(val)})}); const htxt=headers.map(h=>cellText(h).toLowerCase()); const findVal=(keys)=>{const ix=htxt.findIndex(h=>keys.some(k=>h.includes(k))); return ix>=0?fmtDate(row[ix]):''}; obj.inicio=findVal(['inicio','desde','fecha inicio']); obj.termino=findVal(['termino','término','hasta','fecha fin']); obj.fecha=findVal(['fecha']); obj.dias=findVal(['dias','días']); obj.diasDescuento=findVal(['descuento']); obj.observacion=findVal(['observ']); obj.documento=findVal(['documento','resolucion','resolución','orden']); return obj}
function attachGenericDetails(wb){
 const main='Cálculo de días a Cargar';
 const getRows=name=>wb.Sheets[name]?XLSX.utils.sheet_to_json(wb.Sheets[name],{header:1,defval:null}):[];
 wb.SheetNames.filter(n=>n!==main).forEach(sheet=>{
  const rows=getRows(sheet); if(rows.length<2)return;
  let headerIdx=0;
  for(let i=0;i<Math.min(rows.length,10);i++){
   const t=rowText(rows[i]);
   if(t.includes('rut')||t.includes('run')||t.includes('nombre')||t.includes('fecha')){headerIdx=i;break}
  }
  const headers=rows[headerIdx]||[];
  rows.slice(headerIdx+1).forEach(row=>{
   if(!row||row.every(v=>v===null||v===''))return;
   const txtNorm=rowText(row).normalize('NFD').replace(/[\u0300-\u036f]/g,'');
   const txtClean=cleanRun(rowText(row));
   let matched=[];
   funcionarios.forEach((f,idx)=>{
    const runA=cleanRun(f.run), runB=runKey(f.rutSinDv,f.dv), nm=normalizeName(f.nombre);
    const nameParts=nm.split(' ').filter(x=>x.length>3);
    const nameHit=nm&&nameParts.length>=2&&nameParts.slice(0,2).every(part=>txtNorm.includes(part));
    if((runA&&txtClean.includes(runA))||(runB&&txtClean.includes(runB))||nameHit)matched.push(idx)
   });
   matched.forEach(idx=>{
    const ev=makeGenericEvent(sheet,headers,row); ev.generico=true;
    funcionarios[idx].eventos=funcionarios[idx].eventos||[];
    const sig=JSON.stringify(ev.campos);
    if(!funcionarios[idx].eventos.some(e=>JSON.stringify(e.campos||[])===sig))funcionarios[idx].eventos.push(ev);
   });
  });
 });
}
function params(){const anioEl=document.getElementById('anio'); const fin=getFinanzas(); const year=anioEl&&anioEl.value?+anioEl.value:new Date().getFullYear(); return{mes:'',anio:year,inicial:saldoFinancieroBase(fin)}}
function detalleTexto(c){let partes=[]; descuentos.forEach(m=>{if(num(c.detalle?.[m])>0)partes.push(`${m}: -${num(c.detalle[m])} día(s)`)}); if(num(c.horasExtra)>0)partes.push(`Horas Extraordinarias: +${num(c.horasExtra)} día(s)`); if(num(c.reintegros)>0)partes.push(`Reintegro: +${num(c.reintegros)} día(s)`); if(c.observacion)partes.push(`Obs.: ${c.observacion}`); return partes.join(' | ')}
function computed(f){
  let c=JSON.parse(JSON.stringify(f));
  c.diasHabiles=num(c.diasHabiles);
  c.montoDiario=num(c.montoDiario);
  c.detalle=c.detalle||{};
  c.descuentos=descuentos.reduce((a,m)=>a+num(c.detalle[m]),0);
  c.horasExtra=num(c.horasExtra);
  c.reintegros=num(c.reintegros);
  c.aumentos=c.horasExtra+c.reintegros;
  c.totalDiasCalculado=Math.max(0,c.diasHabiles-c.descuentos+c.aumentos);
  // Regla principal v4: se respeta el “Total días a cargar” que viene desde la planilla Excel.
  // Ese campo es el resultado validado de la planilla madre; el detalle de descuentos queda para trazabilidad.
  // Si no existe ese total en el Excel, recién ahí se calcula con la fórmula de respaldo.
  c.totalDias=(f.totalDiasOriginal!==null&&f.totalDiasOriginal!==undefined&&String(f.totalDiasOriginal)!=='')?num(f.totalDiasOriginal):c.totalDiasCalculado;
  c.total=c.totalDias*c.montoDiario;
  c.difExcel=(c.totalOriginal!==null&&c.totalOriginal!==undefined)?c.total-num(c.totalOriginal):0;
  c.difDias=c.totalDias-c.totalDiasCalculado;
  c.motivos=detalleTexto(c)||'Sin movimiento';
  return c
}
function setEstado(e,accion,comentario){flujo.estado=e; estadoFlujo.value=e; flujo.historial.unshift({fecha:new Date().toLocaleString('es-CL'),perfil:perfil.value,accion,comentario:comentario||''}); render()}
function recalcularPlanilla(){if(!funcionarios.length){alert('Primero importa una planilla.');return} render(); toastMsg('Planilla recalculada. Los filtros no alteran los totales.');}
function importarExcel(e){
 if(!canWorkAsAnalyst()){alert('Solo el Analista puede importar planillas.'); e.target.value=''; return}
 const file=e.target.files[0]; if(!file)return;
 const reader=new FileReader();
 reader.onload=evt=>{
  const wb=XLSX.read(evt.target.result,{type:'array',cellDates:true});
  const ws=wb.Sheets['Cálculo de días a Cargar']||wb.Sheets[wb.SheetNames[0]];
  const rows=XLSX.utils.sheet_to_json(ws,{header:1,defval:null});
  funcionarios=[]; archivoInfo={nombre:file.name,hojas:wb.SheetNames,fecha:new Date().toLocaleString('es-CL')};
  const mesEl=document.getElementById('mes');
  const anioEl=document.getElementById('anio');
  if(rows[1]){
    if(mesEl && rows[1][2]) mesEl.value=String(rows[1][2]).toLowerCase().replace(/^./,s=>s.toUpperCase());
    if(anioEl && rows[1][6]) anioEl.value=rows[1][6];
  }
  for(let r=5;r<rows.length;r++){
   const row=rows[r]; if(!row||!row[1])continue;
   const det={'Feriado Legal':num(row[7]),'Permisos Adm.':num(row[8]),'Descanso Complementario':num(row[9]),'Otros Permisos':num(row[10]),'Permisos sin goce':num(row[11]),'Cometidos/Comisiones':num(row[12]),'Capacitaciones':num(row[13]),'Licencias Médicas':num(row[14])};
   funcionarios.push({numero:row[0],nombre:row[1],run:row[2],rutSinDv:row[3],dv:row[4],escala:row[5],diasHabiles:num(row[6]),detalle:det,horasExtra:num(row[15]),reintegros:num(row[16]),totalDiasOriginal:num(row[17]),montoDiario:num(row[18]),totalOriginal:row[19]===null?null:num(row[19]),observacion:'',eventos:[]});
  }
  const byRun={}; funcionarios.forEach((f,i)=>{byRun[runKey(f.rutSinDv,f.dv)]=i; byRun[cleanRun(f.run)]=i;});
  const addEvento=(run,dv,tipo,ev)=>{const k=runKey(run,dv); const i=byRun[k]??byRun[cleanRun(run)]; if(i!==undefined)funcionarios[i].eventos.push({tipo,...ev});};
  const sheetRows=name=>wb.Sheets[name]?XLSX.utils.sheet_to_json(wb.Sheets[name],{header:1,defval:null}):[];
  sheetRows('LICENCIAS').slice(1).forEach(r=>{if(r[1])addEvento(r[1],r[2],'Licencia médica',{documento:r[0],nombre:[r[5],r[3],r[4]].filter(Boolean).join(' ').replace(/\s+/g,' ').trim(),inicio:fmtDate(r[6]),termino:fmtDate(r[7]),dias:r[8],diasHabiles:r[9],diasDescuento:r[10],observacion:r[11]||''})});
  sheetRows('PERMISOS').slice(1).forEach(r=>{if(r[2]){const mov=String(r[10]||'').trim().toUpperCase(); let motivo='Otros Permisos'; if(mov.includes('FERIADO'))motivo='Feriado Legal'; else if(mov.includes('ADMIN'))motivo='Permisos Adm.'; else if(mov.includes('COMP'))motivo='Descanso Complementario'; else if(mov.includes('SIN GOCE'))motivo='Permisos sin goce'; addEvento(r[2],'',motivo,{documento:r[0],nombre:[r[5],r[3],r[4]].filter(Boolean).join(' ').replace(/\s+/g,' ').trim(),inicio:fmtDate(r[6]),termino:fmtDate(r[7]),dias:r[8],diasDescuento:r[8],descuentoMonto:num(r[9]),tipoMovimiento:r[10]||'',tipoDocumento:r[11]||'',numeroDocumento:r[12]||'',fechaDocumento:fmtDate(r[13]),horasSolicitadas:r[14]||'',observacion:r[15]||'',pasado:r[16]||''})}});
  sheetRows('COMISIONES').slice(2).forEach(r=>{if(r[1])addEvento(r[1],'','Cometidos/Comisiones',{calidad:r[0]||'',nombre:[r[4],r[2],r[3]].filter(Boolean).join(' ').replace(/\s+/g,' ').trim(),inicio:fmtDate(r[5]),termino:fmtDate(r[6]),dias:r[7],descuentoMonto:r[8]||0,viatico100:r[9]||0,viatico40:r[10]||0,viatico60:r[11]||0,diasDescuento:r[12]||'',resolucion:r[13]||'',fechaResolucion:fmtDate(r[14]),ciudad:r[15]||'',observacion:r[16]||'',pasado:r[18]||''})});
  sheetRows('HORAS EXTRA').slice(2).forEach(r=>{if(r[2]){const nombre=String(r[2]).toLowerCase(); const idx=funcionarios.findIndex(f=>String(f.nombre||'').toLowerCase().includes(nombre)||nombre.includes(String(f.nombre||'').toLowerCase())); if(idx>=0)funcionarios[idx].eventos.push({tipo:'Horas extraordinarias',orden:r[0],fecha:fmtDate(r[1]),funcionario:r[2],ingreso:r[3]||'',salida:r[4]||'',horas:r[5]||'',carga:r[6]||'',respaldo:r[7]||''});}});
  sheetRows('REINTEGROS').slice(1).forEach(r=>{if(r[1])addEvento(r[1],r[2],'Reintegro',{documento:r[0],nombre:[r[3],r[4],r[5]].filter(Boolean).join(' ').replace(/\s+/g,' ').trim(),inicio:fmtDate(r[6]),termino:fmtDate(r[7]),dias:r[8],valor:r[9],observacion:r[10]||'',pasado:r[11]||''})});
  sheetRows('OBSERVACIONES').slice(4).forEach(r=>{if(r[0]){const nom=[r[0],r[1],r[2]].filter(Boolean).join(' ').replace(/\s+/g,' ').trim().toLowerCase(); const idx=funcionarios.findIndex(f=>String(f.nombre||'').toLowerCase().includes(nom)||nom.includes(String(f.nombre||'').toLowerCase())); if(idx>=0)funcionarios[idx].eventos.push({tipo:'Observación / saldo pendiente',nombre:[r[0],r[1],r[2]].filter(Boolean).join(' '),dias:r[3],monto:r[4],observacion:r[5]||''});}});
  attachGenericDetails(wb);
  planillaActualId=null; datosProcesoAsignados=false; setEstado('Planilla importada','Importó planilla',`${file.name} · ${funcionarios.length} funcionarios · detalle leído desde ${wb.SheetNames.length} hojas`);
  toastMsg('Planilla importada correctamente, con detalle desde las hojas auxiliares.');
 };
 reader.readAsArrayBuffer(file)
}
function filtrados(){const q=cleanRun(buscar.value); const mot=filtroMotivo.value; const res=filtroResultado.value; return funcionarios.map((f,i)=>({f:computed(f),i})).filter(o=>{const f=o.f; let ok=!q||cleanRun(f.run).includes(q)||String(f.nombre||'').toLowerCase().includes(q); if(mot==='Sin movimiento')ok=ok&&f.descuentos===0&&f.aumentos===0; else if(mot==='Reintegro')ok=ok&&f.reintegros>0; else if(mot==='Horas Extraordinarias')ok=ok&&f.horasExtra>0; else if(mot)ok=ok&&num(f.detalle[mot])>0; if(res==='cero')ok=ok&&f.total===0; if(res==='con_descuento')ok=ok&&f.descuentos>0; if(res==='con_aumento')ok=ok&&f.aumentos>0; if(res==='sin_descuento')ok=ok&&f.descuentos===0; return ok})}

function setDisabled(id, disabled){const el=document.getElementById(id); if(el)el.disabled=disabled;}
function aplicarPermisosRol(){
  const analyst = canWorkAsAnalyst();
  const jefe = isJefeDepto() || isJefeDivision();
  const admin = canManageUsers();
  setDisabled('excelFile', !analyst);
  ['mes','anio','montoInicial','obsGeneral'].forEach(id=>setDisabled(id, !analyst));
  document.querySelectorAll('.analystOnly').forEach(el=>el.classList.toggle('hidden', !analyst));
  document.querySelectorAll('.reviewerOnly').forEach(el=>el.classList.toggle('hidden', !jefe));
  const review=document.getElementById('reviewDashboard'); if(review) review.classList.toggle('hidden', !jefe);
  const summary=document.getElementById('summarySection'); if(summary) summary.classList.toggle('hidden', admin && !jefe && !analyst);
  const adminEl=document.getElementById('adminCard'); if(adminEl)adminEl.classList.toggle('hidden',!admin);
  const msgId='roleHelpBox';
  let box=document.getElementById(msgId);
  if(!box){box=document.createElement('div'); box.id=msgId; box.className='note small'; const top=document.querySelector('#appMain .topuser'); if(top)top.after(box);}
  if(admin) box.innerHTML='<b>Perfil Administrador General:</b> puede crear cuentas y asignar perfiles. No revisa ni modifica planillas desde este usuario.';
  else if(analyst) box.innerHTML='<b>Perfil Analista:</b> panel operativo completo para importar Excel, revisar detalles, modificar casos puntuales, exportar y enviar a validación.';
  else if(isJefeDepto()) box.innerHTML='<b>Perfil Jefe Departamento:</b> bandeja resumida de revisión. Solo puede ver la planilla, validar técnicamente o devolver al analista.';
  else if(isJefeDivision()) box.innerHTML='<b>Perfil Jefe División:</b> bandeja resumida de aprobación. Solo puede ver la planilla, aprobar o rechazar/devolver.';
  else box.innerHTML='Perfil no reconocido.';
}

function puedeRevisarJefatura(){return isJefeDepto() || isJefeDivision();}
function alertaEtapaJefatura(){
  if(isJefeDepto()){
    if(flujo.estado==='Enviado a validación técnica') return ['ok','Tiene una planilla para su validación técnica.'];
    if(flujo.estado==='Sin planilla importada') return ['warn','Aún no existe una planilla importada por el analista.'];
    if(flujo.estado==='Planilla importada') return ['warn','La planilla está en preparación del analista; aún no ha sido enviada a validación.'];
    if(flujo.estado==='Validado técnicamente') return ['info','Esta planilla ya fue validada técnicamente y quedó pendiente de aprobación de la División.'];
    if(flujo.estado==='Aprobado para carga') return ['ok','La planilla ya fue aprobada para carga.'];
    if(flujo.estado==='Devuelto a analista') return ['warn','La planilla fue devuelta al analista para corrección.'];
    return ['warn',flujo.estado];
  }
  if(isJefeDivision()){
    if(flujo.estado==='Validado técnicamente') return ['ok','Tiene una planilla validada técnicamente para aprobación final.'];
    if(flujo.estado==='Enviado a validación técnica') return ['warn','La planilla aún se encuentra en revisión del Jefe de Departamento.'];
    if(flujo.estado==='Planilla importada') return ['warn','La planilla todavía está en preparación del analista.'];
    if(flujo.estado==='Aprobado para carga') return ['ok','La planilla ya fue aprobada para carga.'];
    if(flujo.estado==='Rechazado por jefatura') return ['warn','La planilla fue rechazada/devuelta por jefatura.'];
    if(flujo.estado==='Sin planilla importada') return ['warn','Aún no existe una planilla importada por el analista.'];
    return ['warn',flujo.estado];
  }
  return ['warn','Sin etapa asignada.'];
}
function renderReviewDashboard(all,total){
  const cont=document.getElementById('reviewContent'); if(!cont) return;
  if(!puedeRevisarJefatura()){cont.innerHTML='';return;}
  const lista=planillasParaRol();
  const titulo=isJefeDepto()?'Bandeja de validación técnica':'Bandeja de aprobación final';
  const rolTxt=isJefeDepto()?'validar técnicamente':'aprobar finalmente';
  if(!lista.length){cont.innerHTML=`<div class="emptyReview"><h2>${titulo}</h2><p>No hay planillas pendientes o disponibles para este perfil.</p></div>`;return;}
  const pl=lista.find(x=>x.id===planillaActualId);
  if(!pl){
    const pendientes=isJefeDepto()?lista.filter(x=>(x.flujo?.estado)==='Enviado a validación técnica').length:lista.filter(x=>(x.flujo?.estado)==='Validado técnicamente').length;
    cont.innerHTML=`
      <div class="reviewPanel">
        <p class="reviewTitle">${titulo}</p>
        <p><span class="pill ${pendientes?'ok':'info'}">${lista.length}</span> Tiene ${lista.length} planilla(s) disponible(s) en su bandeja. ${pendientes?`Pendientes por ${rolTxt}: ${pendientes}.`:'No hay planillas pendientes de decisión inmediata, pero puede revisar las disponibles.'}</p>
        <div class="readonlyBanner"><b>Vista de jefatura:</b> seleccione una planilla para ver su resumen, buscar funcionarios y registrar una decisión. No puede importar, modificar, eliminar ni exportar.</div>
        <div class="planillaList">${lista.map(x=>{const est=x.flujo?.estado||''; const pendiente=(isJefeDepto()&&est==='Enviado a validación técnica')||(isJefeDivision()&&est==='Validado técnicamente'); return `<div class="planillaItem"><div style="display:flex;justify-content:space-between;gap:10px;align-items:start"><div><b>${x.nombre||'Sin identificador'}</b><br><span class="small">${x.mes||''} ${x.anio||''} · ${x.cantidad||0} funcionarios · Analista: ${x.analista||''}</span><br><span class="pill ${x.eliminada?'danger':(pendiente?'ok':'info')}">${x.eliminada?'Eliminada por administrador':est}</span>${x.eliminada?`<br><span class="small"><b>Motivo eliminación:</b> ${x.eliminacionMotivo||''}</span>`:''}</div><button class="secondary mini" onclick="seleccionarPlanillaRevision('${x.id}')">Seleccionar y revisar</button></div></div>`}).join('')}</div>
      </div>`;
    return;
  }
  const arr=(pl.funcionarios||[]).map(computed);
  const q=normalizeName(reviewSearch);
  const vista=arr.filter(f=>!q||normalizeName(f.nombre).includes(q)||cleanRun(f.run).includes(cleanRun(q)));
  const totalPl=arr.reduce((a,f)=>a+f.total,0);
  const conDesc=arr.filter(f=>f.descuentos>0).length;
  const conAum=arr.filter(f=>f.aumentos>0).length;
  const difsList=arr.filter(f=>Math.abs(f.difExcel)>0);
  const difs=difsList.length;
  const estado=pl.eliminada?'Eliminada por administrador':(pl.flujo?.estado||flujo.estado);
  const puedeValidar=!pl.eliminada&&isJefeDepto()&&estado==='Enviado a validación técnica';
  const puedeAprobar=!pl.eliminada&&isJefeDivision()&&estado==='Validado técnicamente';
  const accionHTML=isJefeDepto()?`
      <button class="ok" onclick="validarTecnica()" ${puedeValidar?'':'disabled'}>Validar técnicamente</button>
      <button class="warn" onclick="devolverAnalista()" ${puedeValidar?'':'disabled'}>Devolver a analista</button>`:`
      <button class="ok" onclick="aprobarFinal()" ${puedeAprobar?'':'disabled'}>Aprobar carga</button>
      <button class="danger" onclick="rechazarFinal()" ${puedeAprobar?'':'disabled'}>Rechazar / devolver</button>`;
  const advertencia=difs?`<div class="alertDiff"><b>Advertencia:</b> esta planilla tiene ${difs} diferencia(s) versus el total original del Excel. <button class="danger mini" onclick="abrirDiferenciasPlanilla()">Ver diferencias específicas</button></div>`:'';
  cont.innerHTML=`
    <div class="reviewHero">
      <div class="reviewPanel">
        <p class="reviewTitle">${titulo}</p>
        <p><span class="pill ${puedeValidar||puedeAprobar?'ok':'warn'}">${puedeValidar||puedeAprobar?'PENDIENTE':'SOLO REVISIÓN'}</span> Planilla seleccionada: <b>${pl.nombre||'Sin identificador'}</b></p>
        <div class="readonlyBanner"><b>Vista de jefatura:</b> solo revisión. No puede importar, modificar, eliminar ni exportar.</div>
        <div class="actions"><button class="secondary" onclick="planillaActualId=null; funcionarios=[]; flujo={estado:'Sin planilla importada',historial:[]}; render();">Volver a bandeja</button></div>
        <div class="grid" style="margin-top:12px">
          <div><label>Buscar persona en esta planilla</label><input id="buscarJefatura" value="${reviewSearch||''}" placeholder="Nombre o RUN" oninput="reviewSearch=this.value;renderReviewMiniTable()"></div>
          <div><label>Mes</label><input value="${pl.mes||''} ${pl.anio||''}" readonly></div>
          <div class="wide"><label>Identificador</label><input value="${pl.nombre||''}" readonly></div>
        </div>
        <div class="kpis" style="grid-template-columns:repeat(3,1fr);margin-top:12px">
          <div class="kpi"><span>Funcionarios</span><strong>${arr.length}</strong></div>
          <div class="kpi"><span>Total a cargar</span><strong>${money(totalPl)}</strong></div>
          <div class="kpi"><span>Estado</span><strong style="font-size:15px">${estado}</strong></div>
          <div class="kpi"><span>Con descuentos</span><strong>${conDesc}</strong></div>
          <div class="kpi"><span>Con aumentos/reintegros</span><strong>${conAum}</strong></div>
          <div class="kpi"><span>Diferencias vs Excel</span><strong>${difs}</strong></div>
        </div>
        ${advertencia}
        <div class="actions"><button class="secondary" onclick="abrirResumenPlanilla()">Ver detalles de planilla</button><button class="secondary" onclick="abrirDetalleObservaciones()">Ver historial</button></div>
      </div>
      <div class="decisionBox"><h2>Decisión</h2><label>Comentario / motivo</label><input id="comentarioJefatura" placeholder="Ej: se valida sin observaciones / devolver por inconsistencia..." oninput="comentarioFlujo.value=this.value"><div class="actions">${accionHTML}</div><p class="small">La decisión quedará registrada en el historial de la planilla seleccionada.</p></div>
    </div>
    <div id="reviewMiniTable" class="tablebox" style="margin-top:14px;max-height:420px"><table><thead><tr><th>N°</th><th>Nombre</th><th>RUN</th><th>Días</th><th>Descuentos</th><th>Aumentos</th><th>Total a cargar</th><th>Diferencia vs Excel</th><th>Motivos</th><th>Detalle</th></tr></thead><tbody id="reviewMiniTbody">${vista.map((f,i)=>`<tr><td>${i+1}</td><td>${f.nombre||''}</td><td>${f.run||''}</td><td>${f.totalDias}</td><td>${f.descuentos}</td><td>${f.aumentos}</td><td><b>${money(f.total)}</b></td><td>${Math.abs(f.difExcel)>0?`<span class="pill warn">${money(f.difExcel)}</span>`:'-'}</td><td>${f.motivos}</td><td><button class="secondary mini" onclick="abrirDetalle(${arr.findIndex(a=>a.run===f.run && a.nombre===f.nombre)})">Detalle</button></td></tr>`).join('')||'<tr><td colspan="10">No hay coincidencias.</td></tr>'}</tbody></table></div>`;
}

function renderReviewMiniTable(){
  const tbody=document.getElementById('reviewMiniTbody');
  if(!tbody || !planillaActualId) return;
  const pl=getPlanillas().find(x=>x.id===planillaActualId);
  if(!pl) return;
  const arr=(pl.funcionarios||[]).map(computed);
  const q=normalizeName(reviewSearch);
  const vista=arr.filter(f=>!q||normalizeName(f.nombre).includes(q)||cleanRun(f.run).includes(cleanRun(q)));
  tbody.innerHTML=vista.map((f,i)=>`<tr><td>${i+1}</td><td>${f.nombre||''}</td><td>${f.run||''}</td><td>${f.totalDias}</td><td>${f.descuentos}</td><td>${f.aumentos}</td><td><b>${money(f.total)}</b></td><td>${Math.abs(f.difExcel)>0?`<span class="pill warn">${money(f.difExcel)}</span>`:'-'}</td><td>${f.motivos}</td><td><button class="secondary mini" onclick="abrirDetalle(${arr.findIndex(a=>a.run===f.run && a.nombre===f.nombre)})">Detalle</button></td></tr>`).join('')||'<tr><td colspan="10">No hay coincidencias.</td></tr>';
}

function abrirDiferenciasPlanilla(){
 const arr=funcionarios.map(computed).filter(f=>Math.abs(f.difExcel)>0);
 if(!arr.length){alert('La planilla seleccionada no presenta diferencias versus Excel.');return}
 detalleFuncionario.innerHTML=`<h3>Diferencias específicas versus Excel</h3><div class="warnbox">Se muestran solo los funcionarios cuya modificación en la página cambió el total respecto del valor original importado desde el Excel.</div><div class="tablebox" style="max-height:520px"><table><thead><tr><th>Nombre</th><th>RUN</th><th>Total actual</th><th>Total original Excel</th><th>Diferencia</th><th>Observación</th></tr></thead><tbody>${arr.map(f=>`<tr><td>${f.nombre||''}</td><td>${f.run||''}</td><td>${money(f.total)}</td><td>${money(f.totalOriginal||0)}</td><td><span class="pill warn">${money(f.difExcel)}</span></td><td>${f.observacion||''}</td></tr>`).join('')}</tbody></table></div>`;
 modalDetalle.style.display='flex';
}
function abrirResumenPlanilla(){const el=document.getElementById('reviewMiniTable'); if(el) el.classList.toggle('hidden');}
function abrirDetalleObservaciones(){
  const html=`<h3>Historial del proceso</h3><div class="tablebox" style="max-height:360px"><table><thead><tr><th>Fecha/hora</th><th>Perfil</th><th>Acción</th><th>Comentario</th></tr></thead><tbody>${flujo.historial.map(h=>`<tr><td>${h.fecha}</td><td>${h.perfil}</td><td>${h.accion}</td><td>${h.comentario}</td></tr>`).join('')||'<tr><td colspan="4">Sin movimientos registrados.</td></tr>'}</tbody></table></div>`;
  detalleFuncionario.innerHTML=html; modalDetalle.style.display='flex';
}

function render(){syncPerfil(); renderUsers(); aplicarPermisosRol(); const anioEl=document.getElementById('anio'); if(anioEl&&!anioEl.value) anioEl.value=new Date().getFullYear(); const anioAuto=document.getElementById('anioAutoVista'); if(anioAuto) anioAuto.value=(anioEl&&anioEl.value)||new Date().getFullYear(); const all=funcionarios.map(computed); const data=filtrados(); vistaActual.value=`${data.length} de ${all.length} registros`; tbody.innerHTML=data.map((o,ix)=>{const f=o.f; const dif=f.difExcel===0?'':`<span class="pill ${Math.abs(f.difExcel)>0?'warn':'ok'}">${money(f.difExcel)}</span>`; const editBtns=canWorkAsAnalyst()?` <button class="ok mini" onclick="abrirModificar(${o.i})">Modificar</button> <button class="danger mini" onclick="eliminarReal(${o.i})">Eliminar</button>`:''; return `<tr><td>${ix+1}</td><td>${f.nombre||''}</td><td>${f.run||''}</td><td>${f.escala||''}</td><td>${f.diasHabiles}</td><td>${f.descuentos}</td><td>${f.horasExtra}</td><td>${f.reintegros}</td><td><b>${f.totalDias}</b></td><td>${money(f.montoDiario)}</td><td><b>${money(f.total)}</b></td><td>${dif}</td><td>${f.motivos}</td><td><button class="secondary mini" onclick="abrirDetalle(${o.i})">Detalle</button>${editBtns}</td></tr>`}).join(''); const total=all.reduce((a,f)=>a+f.total,0); kFun.textContent=all.length; kDiasBase.textContent=all.reduce((a,f)=>a+f.diasHabiles,0); kDesc.textContent=all.reduce((a,f)=>a+f.descuentos,0); kAum.textContent=all.reduce((a,f)=>a+f.aumentos,0); kTotal.textContent=money(total); kSaldo.textContent=money(saldoFinanzas()); renderFinanzas(); estadoFlujo.value=flujo.estado; perfilVista.value=perfil.value; estadoVista.value=flujo.estado; if(document.getElementById('datosAsignadosVista')) datosAsignadosVista.value=datosProcesoAsignados?'Asignado a '+(planillaNombre.value||'planilla'):'Pendiente de asignar'; renderValidaciones(all,total); renderHistorial(); renderFlujo(); renderBotones(); renderReviewDashboard(all,total); renderSeguimientoAnalista(); infoImport.innerHTML=archivoInfo.nombre?`<b>Archivo:</b> ${archivoInfo.nombre}<br><b>Importado:</b> ${archivoInfo.fecha}<br><b>Hojas detectadas:</b> ${archivoInfo.hojas.join(', ')}<br><b>Funcionarios cargados:</b> ${all.length}`:'Aún no se ha importado ninguna planilla.'}
function renderDetalle(all){const map={}; motivos.forEach(m=>map[m]={dias:0,fun:new Set(),tipo:descuentos.includes(m)?'Descuento':'Aumento'}); all.forEach(f=>{descuentos.forEach(m=>{const v=num(f.detalle[m]); if(v>0){map[m].dias+=v; map[m].fun.add(f.run||f.nombre)}}); if(f.horasExtra>0){map['Horas Extraordinarias'].dias+=f.horasExtra; map['Horas Extraordinarias'].fun.add(f.run||f.nombre)} if(f.reintegros>0){map['Reintegro'].dias+=f.reintegros; map['Reintegro'].fun.add(f.run||f.nombre)}}); tbodyDetalle.innerHTML=Object.entries(map).filter(([_,v])=>v.dias>0).map(([m,v])=>`<tr><td>${m}</td><td><span class="pill ${v.tipo==='Descuento'?'danger':'ok'}">${v.tipo}</span></td><td><b>${v.dias}</b></td><td>${v.fun.size}</td><td>${v.tipo==='Descuento'?'Ver detalle por persona':'-'}</td></tr>`).join('')||'<tr><td colspan="5">No hay descuentos, horas extraordinarias ni reintegros registrados.</td></tr>'}
function renderConsulta(data){if(!data.length){consultaPersona.innerHTML='No hay registros para la consulta actual.';return} if(data.length>12){consultaPersona.innerHTML=`Se muestran ${data.length} registros en la tabla. Usa búsqueda por nombre o RUN para ver una consulta individual.`;return} consultaPersona.innerHTML=data.map(o=>{const f=o.f; return `<div class="note"><b>${f.nombre}</b> · RUN ${f.run}<br>Días hábiles: ${f.diasHabiles} · Descuentos: ${f.descuentos} · Aumentos/Reintegros: ${f.aumentos} · <b>Total: ${money(f.total)}</b><br><span class="small">${f.motivos}</span></div>`}).join('')}
function renderValidaciones(all,total){let items=[]; if(!all.length)items.push(['danger','No existe planilla importada.']); if(all.some(f=>!f.run||!f.nombre))items.push(['danger','Hay registros sin nombre o RUN.']); if(all.some(f=>!f.montoDiario))items.push(['warn','Hay funcionarios sin monto diario en la planilla. Revisar antes de enviar.']); if(all.some(f=>Math.abs(f.difExcel)>0))items.push(['warn','Existen diferencias respecto del total original del Excel. Esto puede deberse a una modificación manual hecha en la página.']); if(all.some(f=>Math.abs(f.difDias)>0))items.push(['warn','Hay diferencias entre el Total días a cargar de la planilla y la fórmula de respaldo. Revisa el detalle por persona si corresponde.']); if(params().inicial>0&&total>params().inicial)items.push(['danger','El total a cargar supera el monto disponible inicial.']); if(!items.length)items.push(['ok','Planilla sin alertas básicas. Lista para revisión técnica.']); validaciones.innerHTML=items.map(x=>`<p><span class="pill ${x[0]}">${x[0].toUpperCase()}</span> ${x[1]}</p>`).join('')}
function renderHistorial(){historial.innerHTML=flujo.historial.map(h=>`<tr><td>${h.fecha}</td><td>${h.perfil}</td><td>${h.accion}</td><td>${h.comentario}</td></tr>`).join('')||'<tr><td colspan="4">Sin movimientos registrados.</td></tr>'}
function renderFlujo(){['stImport','stCalc','stVal','stApr'].forEach(id=>document.getElementById(id).className='step'); if(flujo.estado==='Sin planilla importada')stImport.className='step active'; else if(flujo.estado==='Planilla importada'){stImport.className='step done';stCalc.className='step active'} else if(['Devuelto a analista'].includes(flujo.estado)){stImport.className='step done';stCalc.className='step active'} else if(flujo.estado==='Enviado a validación técnica'){stImport.className='step done';stCalc.className='step done';stVal.className='step active'} else if(flujo.estado==='Validado técnicamente'){stImport.className='step done';stCalc.className='step done';stVal.className='step done';stApr.className='step active'} else if(['Aprobado para carga','Rechazado por jefatura'].includes(flujo.estado)){stImport.className='step done';stCalc.className='step done';stVal.className='step done';stApr.className='step done'}}
function renderBotones(){const e=flujo.estado; btnEnviar.disabled=!(canWorkAsAnalyst()&&funcionarios.length&&['Devuelto a analista','Planilla importada'].includes(e)); btnValidar.disabled=!(isJefeDepto()&&e==='Enviado a validación técnica'); btnDevolver.disabled=!(isJefeDepto()&&e==='Enviado a validación técnica'); btnAprobar.disabled=!(isJefeDivision()&&e==='Validado técnicamente'); btnRechazar.disabled=!(isJefeDivision()&&e==='Validado técnicamente')}
function eliminarReal(idx){if(!canWorkAsAnalyst()){alert('Solo el Analista puede eliminar registros.');return} if(flujo.estado!=='Planilla importada'&&flujo.estado!=='Devuelto a analista'){alert('No se puede eliminar registros una vez enviado a validación.');return} if(confirm('¿Eliminar este registro?')){funcionarios.splice(idx,1);render()}}

function puedeEditar(){return canWorkAsAnalyst()&&['Planilla importada','Devuelto a analista'].includes(flujo.estado)}
function cerrarModal(id){document.getElementById(id).style.display='none'}
function abrirModificar(idx){
 if(!puedeEditar()){alert('Solo se puede modificar antes de enviar a validación o cuando el proceso fue devuelto al analista.');return}
 editIdx=idx; const f=funcionarios[idx]; const c=computed(f);
 editNombre.innerHTML=`<b>${c.nombre}</b> · RUN ${c.run} · Total actual: <b>${money(c.total)}</b><br>El cambio queda registrado como ajuste manual del analista.`;
 editDias.value=c.diasHabiles; editFeriado.value=num(c.detalle['Feriado Legal']); editPermAdm.value=num(c.detalle['Permisos Adm.']); editDescanso.value=num(c.detalle['Descanso Complementario']); editOtros.value=num(c.detalle['Otros Permisos']); editSinGoce.value=num(c.detalle['Permisos sin goce']); editComisiones.value=num(c.detalle['Cometidos/Comisiones']); editCapacitaciones.value=num(c.detalle['Capacitaciones']); editLicencias.value=num(c.detalle['Licencias Médicas']); editHoras.value=c.horasExtra; editReintegros.value=c.reintegros; editMonto.value=c.montoDiario; editTotalDias.value=c.totalDias; editObs.value=f.observacion||'';
 modalEditar.style.display='flex';
 calcularEdit();
}
function calcularEdit(){const d=num(editDias.value); const desc=num(editFeriado.value)+num(editPermAdm.value)+num(editDescanso.value)+num(editOtros.value)+num(editSinGoce.value)+num(editComisiones.value)+num(editCapacitaciones.value)+num(editLicencias.value); editTotalDias.value=Math.max(0,d-desc+num(editHoras.value)+num(editReintegros.value));}
function guardarEdit(){
 if(editIdx===null)return; const f=funcionarios[editIdx]; const antes=computed(f);
 f.diasHabiles=num(editDias.value); f.detalle={'Feriado Legal':num(editFeriado.value),'Permisos Adm.':num(editPermAdm.value),'Descanso Complementario':num(editDescanso.value),'Otros Permisos':num(editOtros.value),'Permisos sin goce':num(editSinGoce.value),'Cometidos/Comisiones':num(editComisiones.value),'Capacitaciones':num(editCapacitaciones.value),'Licencias Médicas':num(editLicencias.value)};
 f.horasExtra=num(editHoras.value); f.reintegros=num(editReintegros.value); f.montoDiario=num(editMonto.value); f.totalDiasOriginal=num(editTotalDias.value); f.observacion=editObs.value||'Ajuste manual realizado en página'; f.ajustadoManual=true;
 f.eventos=f.eventos||[]; f.eventos.unshift({tipo:'Ajuste manual',fecha:new Date().toLocaleString('es-CL'),observacion:f.observacion,antes:`${antes.totalDias} días / ${money(antes.total)}`,despues:`${num(editTotalDias.value)} días / ${money(num(editTotalDias.value)*num(editMonto.value))}`});
 flujo.historial.unshift({fecha:new Date().toLocaleString('es-CL'),perfil:perfil.value,accion:'Modificó funcionario',comentario:`${f.nombre}: ${antes.totalDias} días → ${f.totalDiasOriginal} días`});
 cerrarModal('modalEditar'); render(); toastMsg('Funcionario modificado y recalculado.');
}
function detalleResumenTabla(f){
 const rows=[];
 descuentos.forEach(m=>{const v=num(f.detalle?.[m]); if(v>0)rows.push(`<tr><td><b>${m}</b></td><td>Descuento informado en hoja principal</td><td>${v} día(s)</td><td>${money(v*f.montoDiario)}</td></tr>`)});
 if(num(f.horasExtra)>0)rows.push(`<tr><td><b>Horas Extraordinarias</b></td><td>Aumento informado en hoja principal</td><td>+${f.horasExtra} día(s)</td><td>${money(f.horasExtra*f.montoDiario)}</td></tr>`);
 if(num(f.reintegros)>0)rows.push(`<tr><td><b>Reintegro</b></td><td>Aumento informado en hoja principal</td><td>+${f.reintegros} día(s)</td><td>${money(f.reintegros*f.montoDiario)}</td></tr>`);
 return rows.length?`<h3>Resumen del descuento/aumento importado</h3><div class="tablebox" style="max-height:260px"><table><thead><tr><th>Motivo</th><th>Origen</th><th>Días</th><th>Equivalente</th></tr></thead><tbody>${rows.join('')}</tbody></table></div>`:`<div class="okbox">Este funcionario no registra descuentos, horas extraordinarias ni reintegros en la hoja principal.</div>`;
}
function abrirDetalle(idx){
 const base=funcionarios[idx]; const f=computed(base); const ev=base.eventos||[];
 const resumen=`<div class="note"><b>${f.nombre}</b> · RUN ${f.run}<br>Días hábiles: ${f.diasHabiles} · Descuentos: ${f.descuentos} · Horas extra: ${f.horasExtra} · Reintegros: ${f.reintegros} · Total días: <b>${f.totalDias}</b> · Total a cargar: <b>${money(f.total)}</b><br><span class="small">${f.motivos}</span></div>`;
 const detalleAux=ev.length?`<h3>Detalle encontrado en hojas auxiliares del Excel</h3><div class="tablebox" style="max-height:520px"><table><thead><tr><th>Hoja / motivo</th><th>Fechas</th><th>Días / monto</th><th>Documento / respaldo</th><th>Detalle completo de la fila</th></tr></thead><tbody>${ev.map(x=>{const campos=(x.campos||[]).map(c=>`<b>${c.campo}:</b> ${c.valor}`).join('<br>'); return `<tr><td><b>${x.tipo||''}</b></td><td>${[x.inicio,x.termino].filter(Boolean).join(' al ') || x.fecha || ''}</td><td>${[x.dias?x.dias+' día(s)':'',x.diasHabiles?'Hábiles: '+x.diasHabiles:'',x.diasDescuento?'Desc.: '+x.diasDescuento:'',x.descuentoMonto?money(x.descuentoMonto):'',x.valor?money(x.valor):'',x.monto?money(x.monto):'',x.carga?money(x.carga):''].filter(Boolean).join('<br>')}</td><td>${[x.documento?'N°/Orden: '+x.documento:'',x.numeroDocumento?'Doc.: '+x.numeroDocumento:'',x.tipoMovimiento?'Movimiento: '+x.tipoMovimiento:'',x.tipoDocumento?'Tipo doc.: '+x.tipoDocumento:'',x.fechaDocumento?'Fecha doc.: '+x.fechaDocumento:'',x.resolucion?'Resolución: '+x.resolucion:'',x.fechaResolucion?'Fecha resolución: '+x.fechaResolucion:'',x.ciudad?'Ciudad: '+x.ciudad:'',x.calidad?'Calidad: '+x.calidad:'',x.horas?'Horas: '+x.horas:'',x.ingreso?'Ingreso: '+x.ingreso:'',x.salida?'Salida: '+x.salida:'',x.pasado?'Estado: '+x.pasado:'',x.antes?'Antes: '+x.antes:'',x.despues?'Después: '+x.despues:''].filter(Boolean).join('<br>')}</td><td>${campos || x.observacion || x.respaldo || ''}</td></tr>`}).join('')}</tbody></table></div>`:'<div class="warnbox">No se encontraron filas asociadas en las hojas auxiliares para este funcionario. De todos modos, arriba queda visible el resumen importado desde la hoja principal.</div>';
 detalleFuncionario.innerHTML=resumen+detalleResumenTabla(f)+detalleAux; modalDetalle.style.display='flex';
}

function validarDatosProcesoBasicos(){
 if(!funcionarios.length){alert('Primero importa la planilla Excel.');return false}
 if(!planillaNombre.value.trim()){alert('Debe indicar el identificador de la planilla.'); planillaNombre.focus(); return false}
 return true;
}
function asignarDatosProceso(){
 if(!canWorkAsAnalyst()){alert('Solo el Analista puede asignar el identificador.');return}
 if(!validarDatosProcesoBasicos()) return;
 if(!planillaActualId) planillaActualId='pl_'+Date.now();
 datosProcesoAsignados=true;
 const anioSistema=new Date().getFullYear();
 flujo.historial.unshift({fecha:new Date().toLocaleString('es-CL'),perfil:perfil.value,accion:'Asignó identificador de planilla',comentario:`${planillaNombre.value} · Año automático ${anioSistema}`});
 guardarPlanillaActual();
 render();
 toastMsg('Identificador asignado. Ahora puede enviar a validación.');
}
function seleccionarPlanillaRevision(id){
 const pl=planillasParaRol().find(x=>x.id===id); if(!pl){alert('No se encontró la planilla seleccionada.');return}
 planillaActualId=pl.id; funcionarios=pl.funcionarios||[]; flujo=pl.flujo||{estado:'Sin planilla importada',historial:[]}; archivoInfo=pl.archivoInfo||{nombre:'',hojas:[],fecha:''}; datosProcesoAsignados=!!pl.datosProcesoAsignados; reviewSearch=''; render();
}
function enviarValidacion(){
 if(!canWorkAsAnalyst()){alert('Solo el Analista puede enviar el cálculo a validación.');return}
 if(!validarDatosProcesoBasicos()) return;
 if(!datosProcesoAsignados){alert('Antes de enviar, debe presionar “Asignar identificador” para enlazar el identificador con esta planilla.'); return}
 if(!planillaActualId) planillaActualId='pl_'+Date.now();
 setEstado('Enviado a validación técnica','Subió cálculo a validación',comentarioFlujo.value||`Planilla ${planillaNombre.value} enviada con ${funcionarios.length} funcionarios.`);
 guardarPlanillaActual();
 if(!getPlanillas().some(x=>x.id===planillaActualId)){alert('No se pudo guardar la planilla en el navegador. Revise que el almacenamiento local no esté bloqueado.'); return;}
 comentarioFlujo.value=''; toastMsg('Cálculo enviado a validación técnica y guardado en seguimiento permanente.');
}
function actualizarPlanillaSeleccionada(nuevoEstado,accion,comentario){
 const arr=getPlanillas(); const ix=arr.findIndex(x=>x.id===planillaActualId); if(ix<0){alert('Seleccione una planilla.');return false}
 funcionarios=arr[ix].funcionarios||[]; flujo=arr[ix].flujo||flujo; archivoInfo=arr[ix].archivoInfo||archivoInfo; datosProcesoAsignados=!!arr[ix].datosProcesoAsignados; if(document.getElementById('mes')) mes.value=arr[ix].mes||''; if(document.getElementById('anio')) anio.value=arr[ix].anio||''; if(document.getElementById('montoInicial')) montoInicial.value=arr[ix].inicial||0; if(document.getElementById('obsGeneral')) obsGeneral.value=arr[ix].obs||''; if(document.getElementById('planillaNombre')) planillaNombre.value=arr[ix].nombre||'';
 setEstado(nuevoEstado,accion,comentario); arr[ix]=snapshotPlanilla(); savePlanillas(arr); return true;
}
function validarTecnica(){if(!isJefeDepto()){alert('Solo el Jefe de Departamento puede validar técnicamente.');return} if(actualizarPlanillaSeleccionada('Validado técnicamente','Validó técnicamente',comentarioFlujo.value||'Planilla revisada y validada por Jefe de Departamento.')){comentarioFlujo.value=''; toastMsg('Planilla validada técnicamente.'); render();}}
function devolverAnalista(){if(!isJefeDepto()){alert('Solo el Jefe de Departamento puede devolver al analista.');return} if(actualizarPlanillaSeleccionada('Devuelto a analista','Devolvió a analista',comentarioFlujo.value||'Se devuelve para corrección u observación.')){comentarioFlujo.value=''; toastMsg('Proceso devuelto al analista.'); render();}}
function aprobarFinal(){if(!isJefeDivision()){alert('Solo el Jefe de División puede aprobar la carga.');return} if(actualizarPlanillaSeleccionada('Aprobado para carga','Aprobó carga',comentarioFlujo.value||'Carga aprobada por Jefe de División.')){comentarioFlujo.value=''; toastMsg('Carga aprobada.'); render();}}
function rechazarFinal(){if(!isJefeDivision()){alert('Solo el Jefe de División puede rechazar o devolver.');return} if(actualizarPlanillaSeleccionada('Rechazado por jefatura','Rechazó/devolvió',comentarioFlujo.value||'Se rechaza o devuelve para revisión.')){comentarioFlujo.value=''; toastMsg('Carga rechazada/devuelta.'); render();}}

function planillasAnalista(){
 const arr=getPlanillas();
 if(!currentUser) return [];
 // El seguimiento del analista muestra todas las planillas institucionales enviadas,
 // no solo las creadas en la sesión actual. Así se mantiene la trazabilidad
 // aunque se cierre sesión, se cambie de usuario o haya más de un analista.
 if(isAdmin() || isAnalista()) return arr;
 return arr;
}
function etapaHTML(estado){
 const e=estado||'Sin estado';
 const cls=e.includes('Eliminada')?'danger':(e==='Aprobado para carga'?'ok':(e.includes('Devuelto')||e.includes('Rechazado')?'danger':(e.includes('Validado')?'info':'warn')));
 return `<span class="pill ${cls}">${e}</span>`;
}
function renderSeguimientoAnalista(){
 const cont=document.getElementById('seguimientoAnalista');
 if(!cont) return;
 if(!canWorkAsAnalyst()){cont.innerHTML=''; return;}
 const q=normalizeName(document.getElementById('buscarSeguimiento')?.value||'');
 const f=document.getElementById('filtroSeguimiento')?.value||'';
 let lista=planillasAnalista();
 if(f) lista=lista.filter(x=>(x.flujo?.estado||'')===f);
 if(q) lista=lista.filter(x=>normalizeName([x.nombre,x.mes,x.anio,x.flujo?.estado,x.obs,x.archivoInfo?.nombre].join(' ')).includes(q));
 if(document.getElementById('totalSeguimiento')) totalSeguimiento.value=lista.length;
 if(!lista.length){cont.innerHTML='<div class="emptyReview"><b>No hay planillas para mostrar.</b><br><span class="small">Cuando el analista envíe una planilla a validación, aparecerá en este seguimiento.</span></div>'; return;}
 cont.innerHTML=`<table><thead><tr><th>Planilla</th><th>Mes/Año</th><th>Estado actual</th><th>Funcionarios</th><th>Total</th><th>Última actualización</th><th>Acciones</th></tr></thead><tbody>${lista.map(x=>{
   const aprobado=!x.eliminada&&(x.flujo?.estado||'')==='Aprobado para carga';
   const acciones=`<button class="secondary mini" onclick="abrirSeguimientoPlanilla('${x.id}')">Ver seguimiento</button> ${aprobado?`<button class="ok mini" onclick="descargarMovimientosAprobados('${x.id}')">Descargar movimientos</button> <button class="ok mini" onclick="descargarReporteFinanciero('${x.id}')">Descargar detalle financiero</button>`:''}`;
   return `<tr><td><b>${x.nombre||'Sin identificador'}</b><br><span class="small">${x.archivoInfo?.nombre||''}</span></td><td>${x.mes||''} ${x.anio||''}</td><td>${etapaHTML(x.eliminada?'Eliminada por administrador':x.flujo?.estado)}${x.eliminada?`<br><span class="small"><b>Motivo:</b> ${x.eliminacionMotivo||''}</span>`:''}</td><td>${x.cantidad||0}</td><td><b>${money(x.total||0)}</b></td><td>${x.actualizado||''}</td><td>${acciones}</td></tr>`;
  }).join('')}</tbody></table>`;
}

function abrirSeguimientoPlanilla(id){
 cargarPlanilla(id);
 const btn=[...document.querySelectorAll('.tab')].find(b=>String(b.getAttribute('onclick')||'').includes("validacion"));
 if(btn) showTab('validacion',btn);
}


function planillasAprobadasActivas(){return getPlanillas().filter(x=>!x.eliminada&&(x.flujo?.estado||'')==='Aprobado para carga')}
function renderEdenredModule(){
 const sel=document.getElementById('edenredPlanilla'); if(!sel) return;
 const prev=sel.value;
 const aprobadas=planillasAprobadasActivas();
 sel.innerHTML=aprobadas.length?'<option value="">Seleccione una planilla aprobada</option>'+aprobadas.map(x=>`<option value="${x.id}">${x.nombre||'Sin identificador'} · ${money(x.total||0)} · ${x.cantidad||0} funcionarios</option>`).join(''):'<option value="">No hay planillas aprobadas disponibles</option>';
 if(prev && aprobadas.some(x=>x.id===prev)) sel.value=prev;
 const est=document.getElementById('edenredEstado');
 if(est) est.value=aprobadas.length?'Listo para seleccionar planilla':'Sin planillas aprobadas';
}
function nombreSeguroArchivo(txt){return String(txt||'planilla').replace(/[^a-z0-9áéíóúñ_-]+/gi,'_').replace(/_+/g,'_')}
function mapaMontosPlanilla(pl){
 const map={};
 (pl.funcionarios||[]).map(computed).forEach(f=>{
   const monto=Math.round(Number(f.total)||0);
   if(monto<=0) return;
   const keys=[cleanRun(f.run), runKey(f.rutSinDv,f.dv), cleanRun(String(f.rutSinDv||'')+String(f.dv||''))].filter(Boolean);
   keys.forEach(k=>{map[k]=monto});
 });
 return map;
}
function traspasarEdenred(){
 if(!canWorkAsAnalyst()){alert('Solo el Analista puede generar el Excel de carga Edenred.');return}
 const sel=document.getElementById('edenredPlanilla'); const fileInput=document.getElementById('edenredFile');
 const id=sel?.value||''; const file=fileInput?.files?.[0];
 if(!id){alert('Debe seleccionar una planilla aprobada.'); return}
 if(!file){alert('Debe cargar el Excel base de Edenred.'); return}
 const pl=getPlanillas().find(x=>x.id===id);
 if(!pl || pl.eliminada || (pl.flujo?.estado||'')!=='Aprobado para carga'){alert('La planilla seleccionada no está aprobada para carga.'); return}
 const montoMap=mapaMontosPlanilla(pl);
 const funcionariosCarga=(pl.funcionarios||[]).map(computed).filter(f=>Math.round(Number(f.total)||0)>0).map(f=>({
   run: String(f.run||runKey(f.rutSinDv,f.dv)||'').trim(),
   key: cleanRun(f.run)||runKey(f.rutSinDv,f.dv)||cleanRun(String(f.rutSinDv||'')+String(f.dv||'')),
   nombre: String(f.nombre||f.funcionario||'').trim(),
   monto: Math.round(Number(f.total)||0),
   descuento: Math.round(Number(f.descuento)||0),
   aumento: Math.round(Number(f.aumento)||0),
   reintegro: Math.round(Number(f.reintegro)||0),
   totalDias: Number(f.totalDias)||0,
   diasDescuento: Number(f.diasDescuento)||0
 })).filter(f=>f.key && f.monto>0);
 const aprobadosPorKey={};
 funcionariosCarga.forEach(f=>{aprobadosPorKey[f.key]=f});
 const reader=new FileReader();
 reader.onload=evt=>{
   try{
     const wb=XLSX.read(evt.target.result,{type:'array',cellDates:true});
     const sheetName=wb.SheetNames[0];
     const ws=wb.Sheets[sheetName];
     const rows=XLSX.utils.sheet_to_json(ws,{header:1,defval:''});
     if(!rows.length){alert('El Excel base Edenred está vacío.'); return}
     const header=rows[0].map(x=>String(x||'').trim());
     const rutIx=header.findIndex(h=>normalizeName(h).includes('rut')||normalizeName(h).includes('run'));
     let montoIx=header.findIndex(h=>normalizeName(h).includes('monto'));
     if(rutIx<0){alert('No se encontró una columna Rut/RUN en el Excel de Edenred.'); return}
     if(montoIx<0){header.push('Monto'); montoIx=header.length-1; rows[0]=header;}
     const out=[header];
     const encontradosKeys=new Set();
     let asignados=0, eliminados=0, total=0;
     for(let i=1;i<rows.length;i++){
       const row=(rows[i]||[]).slice();
       while(row.length<header.length) row.push('');
       const rut=cleanRun(row[rutIx]);
       const monto=montoMap[rut];
       if(monto && monto>0){
         row[montoIx]=monto;
         out.push(row);
         encontradosKeys.add(rut);
         asignados++;
         total+=monto;
       } else {
         eliminados++;
       }
     }

     const noEncontrados=funcionariosCarga.filter(f=>!encontradosKeys.has(f.key));

     // Archivo 1: encontrados, listo para carga Edenred, con el formato base.
     const wbCarga=XLSX.utils.book_new();
     const wsCarga=XLSX.utils.aoa_to_sheet(out);
     const rangeCarga=XLSX.utils.decode_range(wsCarga['!ref']||'A1:A1');
     wsCarga['!autofilter']={ref:XLSX.utils.encode_range(rangeCarga)};
     wsCarga['!cols']=header.map((h,ix)=>({wch: ix===0?28:(ix===1?14:(ix===montoIx?12:20))}));
     XLSX.utils.book_append_sheet(wbCarga,wsCarga,sheetName.substring(0,31)||'Carga Edenred');
     descargarWorkbook(wbCarga,`edenred_carga_encontrados_${nombreSeguroArchivo(pl.nombre)}.xlsx`);

     // Archivo 2: funcionarios aprobados que no aparecieron en el Excel base Edenred.
     const faltantesHeader=['RUN/RUT','Funcionario','Monto aprobado','Días considerados','Días descuento','Descuento','Aumento / horas extra','Reintegro','Observación'];
     const faltantesRows=[faltantesHeader].concat(noEncontrados.map(f=>[
       f.run,
       f.nombre,
       f.monto,
       f.totalDias,
       f.diasDescuento,
       f.descuento,
       f.aumento,
       f.reintegro,
       'Funcionario con monto aprobado, pero no encontrado en el Excel base Edenred'
     ]));
     const wbFaltantes=XLSX.utils.book_new();
     const wsFaltantes=XLSX.utils.aoa_to_sheet(faltantesRows);
     const rangeFaltantes=XLSX.utils.decode_range(wsFaltantes['!ref']||'A1:A1');
     wsFaltantes['!autofilter']={ref:XLSX.utils.encode_range(rangeFaltantes)};
     wsFaltantes['!cols']=[{wch:16},{wch:34},{wch:16},{wch:16},{wch:14},{wch:14},{wch:18},{wch:14},{wch:60}];
     XLSX.utils.book_append_sheet(wbFaltantes,wsFaltantes,'No encontrados');
     descargarWorkbook(wbFaltantes,`edenred_no_encontrados_${nombreSeguroArchivo(pl.nombre)}.xlsx`);

     const msg=`Proceso Edenred generado. Encontrados/listos para carga: ${asignados}. No encontrados de la planilla aprobada: ${noEncontrados.length}. Filas del Excel base eliminadas por no tener coincidencia o monto: ${eliminados}. Total encontrado para carga: ${money(total)}.`;
     if(document.getElementById('edenredEstado')) edenredEstado.value=`${asignados} encontrados · ${noEncontrados.length} no encontrados · ${money(total)}`;
     if(document.getElementById('edenredInfo')) edenredInfo.innerHTML=`<b>${msg}</b><br>Se descargaron dos archivos: <b>encontrados/listos para carga</b> y <b>no encontrados</b>. La coincidencia se realizó por RUN/RUT sin puntos ni guion.`;
     toastMsg(msg);
   }catch(err){console.error(err); alert('No fue posible generar los Excel Edenred. Revise que el archivo tenga formato .xlsx válido.');}
 };
 reader.readAsArrayBuffer(file);
}
function descargarWorkbook(wb,nombreArchivo){
 const wbout=XLSX.write(wb,{bookType:'xlsx',type:'array'});
 const blob=new Blob([wbout],{type:'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet'});
 const a=document.createElement('a');
 a.href=URL.createObjectURL(blob);
 a.download=nombreArchivo;
 document.body.appendChild(a); a.click();
 setTimeout(()=>{URL.revokeObjectURL(a.href); a.remove();},700);
}

function descargarMovimientosAprobados(id){
 const pl=getPlanillas().find(x=>x.id===id);
 if(!pl){alert('No se encontró la planilla.');return}
 if((pl.flujo?.estado||'')!=='Aprobado para carga'){alert('Solo se puede descargar el detalle cuando la planilla esté aprobada por el Jefe de División.');return}
 const rows=[];
 rows.push(['Tipo registro','Mes','Año','Identificador planilla','Fecha descarga','Nombre funcionario','RUN','Motivo / movimiento','Fecha inicio','Fecha término','Fecha','Días','Monto asociado','Observación / respaldo','Total funcionario','Estado final']);
 (pl.funcionarios||[]).map(computed).forEach(f=>{
   const totalFunc=f.total||0;
   const evs=f.eventos||[];
   const tieneMov=evs.length || f.motivos!=='Sin movimiento';
   if(evs.length){
     evs.forEach(ev=>{
       const campos=(ev.campos||[]).map(c=>`${c.campo}: ${c.valor}`).join(' | ');
       const monto=num(ev.descuentoMonto)||num(ev.valor)||num(ev.monto)||num(ev.carga)||'';
       rows.push(['Movimiento auxiliar',pl.mes||'',pl.anio||'',pl.nombre||'',new Date().toLocaleString('es-CL'),f.nombre||'',f.run||'',ev.tipo||f.motivos||'',ev.inicio||'',ev.termino||'',ev.fecha||'',ev.dias||ev.diasHabiles||ev.diasDescuento||'',monto,campos||ev.observacion||'',totalFunc,pl.flujo?.estado||'']);
     });
   }
   if(!evs.length && tieneMov){
     rows.push(['Resumen planilla',pl.mes||'',pl.anio||'',pl.nombre||'',new Date().toLocaleString('es-CL'),f.nombre||'',f.run||'',f.motivos||'', '', '', '', f.totalDias||'', totalFunc, f.observacion||'Movimiento informado en hoja principal', totalFunc, pl.flujo?.estado||'']);
   }
 });
 rows.push([]);
 rows.push(['Historial administrativo','','','','Fecha/hora','','','Acción','','','','','', 'Comentario','','Perfil']);
 (pl.flujo?.historial||[]).forEach(h=>rows.push(['Historial','','','',h.fecha||'','','',h.accion||'','','','','','',h.comentario||'','',h.perfil||'']));
 const csv='\ufeff'+rows.map(r=>r.map(v=>'"'+String(v??'').replaceAll('"','""')+'"').join(';')).join('\n');
 const a=document.createElement('a');
 a.href=URL.createObjectURL(new Blob([csv],{type:'text/csv;charset=utf-8'}));
 a.download=`movimientos_aprobados_${(pl.nombre||'planilla').replace(/[^a-z0-9áéíóúñ_-]+/gi,'_')}.csv`;
 a.click();
 toastMsg('Detalle de movimientos aprobado descargado.');
}


function descargarReporteFinanciero(id){
 const pl=getPlanillas().find(x=>x.id===id);
 if(!pl){alert('No se encontró la planilla.');return}
 if((pl.flujo?.estado||'')!=='Aprobado para carga'){
   alert('El detalle financiero solo se puede descargar cuando la planilla esté aprobada por el Jefe de División.');
   return;
 }
 const esc=s=>String(s??'').replace(/[&<>]/g,m=>({'&':'&amp;','<':'&lt;','>':'&gt;'}[m]));
 const moneyPlain=n=>new Intl.NumberFormat('es-CL',{style:'currency',currency:'CLP',maximumFractionDigits:0}).format(Number(n)||0);
 const fecha=new Date().toLocaleDateString('es-CL');
 const funcionariosReporte=(pl.funcionarios||[]).map(computed);
 const totalUtilizado=funcionariosReporte.reduce((a,f)=>a+(Number(f.total)||0),0);
 const montoInicial=Number(pl.inicial)||0;
 const saldo=Math.max(0,montoInicial-totalUtilizado);
 const diferencias=funcionariosReporte.filter(f=>(Number(f.difExcel)||0)!==0);
 const modificacionesManuales=funcionariosReporte.filter(f=>f.ajustadoManual || (f.eventos||[]).some(ev=>String(ev.tipo||'').toLowerCase().includes('ajuste manual')) || f.observacion);
 const filasManual=modificacionesManuales.length?modificacionesManuales.map(f=>{
   const eventos=(f.eventos||[]).filter(ev=>String(ev.tipo||'').toLowerCase().includes('ajuste manual'));
   const detalle=eventos.length?eventos.map(ev=>{
     const partes=[ev.fecha?('Fecha: '+ev.fecha):'', ev.antes?('Antes: '+ev.antes):'', ev.despues?('Después: '+ev.despues):'', ev.observacion?('Observación: '+ev.observacion):''].filter(Boolean);
     return partes.join(' | ');
   }).join('<br>'):(f.observacion||'Modificación manual registrada por el analista.');
   return `<tr><td>${esc(f.nombre||'')}</td><td>${esc(f.run||'')}</td><td>${esc(detalle)}</td><td style="text-align:right;">${moneyPlain(f.totalOriginal)}</td><td style="text-align:right;">${moneyPlain(f.total)}</td><td style="text-align:right;">${moneyPlain(f.difExcel)}</td></tr>`;
 }).join(''):`<tr><td colspan="6">No se registran modificaciones manuales efectuadas en esta planilla.</td></tr>`;
 const filasDif=diferencias.length?diferencias.map(f=>`<tr><td>${esc(f.nombre||'')}</td><td>${esc(f.run||'')}</td><td style="text-align:right;">${moneyPlain(f.totalOriginal)}</td><td style="text-align:right;">${moneyPlain(f.total)}</td><td style="text-align:right;">${moneyPlain(f.difExcel)}</td><td>${esc(f.observacion||'Diferencia detectada entre monto Excel y monto final registrado.')}</td></tr>`).join(''):`<tr><td colspan="6">No se registran diferencias entre el monto original del Excel y el monto final de la planilla aprobada.</td></tr>`;
 const historial=(pl.flujo?.historial||[]).map(h=>`<tr><td>${esc(h.fecha||'')}</td><td>${esc(h.perfil||'')}</td><td>${esc(h.accion||'')}</td><td>${esc(h.comentario||'')}</td></tr>`).join('')||'<tr><td colspan="4">Sin historial registrado.</td></tr>';
 const doc=`<!DOCTYPE html><html><head><meta charset="UTF-8"><title>Reporte Financiero</title><style>
 body{font-family:Arial,Helvetica,sans-serif;font-size:12pt;color:#111;line-height:1.35;} h1{text-align:center;font-size:16pt;} h2{font-size:13pt;margin-top:22px;} table{width:100%;border-collapse:collapse;margin:10px 0;} th,td{border:1px solid #999;padding:6px;vertical-align:top;} th{background:#e9eef7;} .no-border td{border:none;} .right{text-align:right;} .note{font-size:10pt;color:#333;} .firma{margin-top:45px;text-align:center;}
 </style></head><body>
 <h1>Reporte Mensual de Gastos realizado por concepto de Tarjeta de Alimentación</h1>
 <p>Conforme al proceso de carga de la tarjeta de alimentación del personal de la Subsecretaría de Defensa, se informa el detalle financiero asociado a la planilla aprobada <b>${esc(pl.nombre||'Sin identificador')}</b>, identificada como <b>${esc(pl.nombre||'Sin identificador')}</b>.</p>
 <p>Santiago, ${esc(fecha)}</p>
 <h2>Monto inicial disponible para el período</h2>
 <table><tr><th>Concepto</th><th>Monto</th></tr><tr><td>Monto inicial registrado para el período</td><td class="right">${moneyPlain(montoInicial)}</td></tr><tr><td>Total utilizado en planilla aprobada</td><td class="right">${moneyPlain(totalUtilizado)}</td></tr><tr><td><b>Saldo estimado posterior a la carga</b></td><td class="right"><b>${moneyPlain(saldo)}</b></td></tr></table>
 <h2>Modificaciones manuales efectuadas por el analista</h2>
 <table><tr><th>Funcionario</th><th>RUN</th><th>Detalle de modificación</th><th>Monto Excel</th><th>Monto final</th><th>Diferencia</th></tr>${filasManual}</table>
 <h2>Diferencias u observaciones de control</h2>
 <table><tr><th>Funcionario</th><th>RUN</th><th>Monto Excel</th><th>Monto final</th><th>Diferencia</th><th>Observación</th></tr>${filasDif}</table>
 <h2>Historial administrativo de validación</h2>
 <table><tr><th>Fecha</th><th>Perfil</th><th>Acción</th><th>Comentario</th></tr>${historial}</table>
 <p class="note">El presente documento fue generado automáticamente desde el sistema de control de carga de tarjeta de alimentación, una vez aprobada la planilla por el perfil Jefe División.</p>
 <div class="firma"><br><br>____________________________________<br>Jefatura Responsable<br>Subsecretaría de Defensa</div>
 </body></html>`;
 const blob=new Blob(['\ufeff'+doc],{type:'application/msword;charset=utf-8'});
 const a=document.createElement('a');
 a.href=URL.createObjectURL(blob);
 a.download=`detalle_financiero_${String(pl.nombre||'planilla').replace(/[^a-z0-9áéíóúñ_-]+/gi,'_')}.doc`;
 document.body.appendChild(a);
 a.click();
 setTimeout(()=>{URL.revokeObjectURL(a.href); a.remove();},500);
 toastMsg('Detalle financiero descargado.');
}

function exportarCSV(soloFiltrado){if(!canWorkAsAnalyst()){alert('Solo el Analista puede exportar CSV.');return} if(!funcionarios.length){alert('Primero importa una planilla.');return} const p=params(); const base=(soloFiltrado?filtrados().map(o=>o.f):funcionarios.map(computed)); const header=['N','Mes','Año','Nombre','RUN','Rut sin DV','DV','Escala','Días hábiles planilla',...descuentos,'Total descuentos informativos','Horas Extraordinarias','Reintegros','Total aumentos','Total días a cargar Excel/aplicado','Total días fórmula respaldo','Diferencia días','Monto diario','Total a cargar','Total original Excel','Diferencia vs Excel','Detalle motivos','Observación ajuste','Ajustado manual','Estado flujo']; const rows=[header,...base.map((f,i)=>[i+1,p.mes,p.anio,f.nombre,f.run,f.rutSinDv,f.dv,f.escala,f.diasHabiles,...descuentos.map(m=>num(f.detalle[m])),f.descuentos,f.horasExtra,f.reintegros,f.aumentos,f.totalDias,f.totalDiasCalculado,f.difDias,f.montoDiario,f.total,f.totalOriginal??'',f.difExcel,f.motivos,f.observacion||'',f.ajustadoManual?'Sí':'No',flujo.estado])]; const csv='\ufeff'+rows.map(r=>r.map(v=>'"'+String(v??'').replaceAll('"','""')+'"').join(';')).join('\n'); const a=document.createElement('a'); a.href=URL.createObjectURL(new Blob([csv],{type:'text/csv;charset=utf-8'})); a.download=`calculo_tarjeta_${(planillaNombre.value||'planilla').replace(/[^a-z0-9áéíóúñ_-]+/gi,'_')}_${p.anio}_${soloFiltrado?'filtrado':'completo'}.csv`; a.click(); toastMsg('CSV exportado.');}
function limpiarTodo(){if(!canWorkAsAnalyst()){alert('Solo el Analista puede limpiar la planilla.');return} if(confirm('¿Limpiar toda la planilla, filtros y flujo de validación?')){funcionarios=[]; archivoInfo={nombre:'',hojas:[],fecha:''}; flujo={estado:'Sin planilla importada',historial:[]}; planillaActualId=null; datosProcesoAsignados=false; buscar.value='';filtroMotivo.value='';filtroResultado.value='';excelFile.value='';render();toastMsg('Datos limpiados.')}}
function showTab(id,btn){document.querySelectorAll('.tabpane').forEach(x=>x.classList.add('hidden')); const pane=document.getElementById(id); if(pane)pane.classList.remove('hidden'); document.querySelectorAll('.tab').forEach(x=>x.classList.remove('active')); if(btn&&btn.classList)btn.classList.add('active')}
function togglePassword(){const p=document.getElementById('loginPass'); if(!p)return; p.type=p.type==='password'?'text':'password';}
function openModule(id){const btn=[...document.querySelectorAll('.tab')].find(b=>String(b.getAttribute('onclick')||'').includes("'"+id+"'")); showTab(id,btn||null); const sec=document.getElementById('analystTabsSection'); if(sec)sec.scrollIntoView({behavior:'smooth',block:'start'});}
function filterMenu(){const q=(document.getElementById('menuSearch')?.value||'').toLowerCase(); document.querySelectorAll('#sideNav a,#sideNav button').forEach(el=>{el.style.display=el.textContent.toLowerCase().includes(q)||!q?'block':'none';});}
[montoInicial,mes,anio,planillaNombre,buscar,filtroMotivo,filtroResultado].forEach(el=>{el.addEventListener('input',render);el.addEventListener('change',render)});['editDias','editFeriado','editPermAdm','editDescanso','editOtros','editSinGoce','editComisiones','editCapacitaciones','editLicencias','editHoras','editReintegros','editMonto'].forEach(id=>{const el=document.getElementById(id); if(el){el.addEventListener('input',calcularEdit);el.addEventListener('change',calcularEdit)}});restoreSession(); renderUsers(); render();
