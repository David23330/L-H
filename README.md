<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Informe Interactivo SG-SST: Consultorio L&M</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals -->
    <!-- Application Structure Plan: A single-page dashboard design with a sticky top navigation bar for easy access to all sections. The structure prioritizes quick understanding and exploration over the linear format of the source report. It starts with an executive summary (Resumen) for key insights, followed by a detailed company profile (La Empresa) with interactive tabs, an interactive evaluation of the standards (Evaluación), and concludes with the key findings (Conclusiones). This dashboard approach allows users (e.g., management, auditors) to quickly grasp the overall status and then drill down into specific areas of interest, which is more usable and efficient than reading a sequential presentation. -->
    <!-- Visualization & Content Choices: 
        - Resumen (Executive Summary): Goal: Inform/Summarize. Viz: Donut Chart (Chart.js) for compliance ratio and stat cards for key numbers (workers, risk level). Interaction: Hover on chart. Justification: Provides a high-level, scannable overview of the most critical results.
        - La Empresa (The Company): Goal: Organize. Viz: HTML/CSS Tabbed Interface. Interaction: Clickable tabs to switch between 'Estructura' and 'Funcionamiento'. Justification: Neatly organizes a large amount of descriptive information into logical, digestible chunks without cluttering the UI.
        - Evaluación (Standards Evaluation): Goal: Compare/Explore. Viz: Interactive vertical list/accordion (HTML/CSS/JS). Interaction: Click to expand/collapse each standard's details. Justification: This transforms a long, static list into an engaging component that encourages user exploration and direct comparison between standards. Color-coding (green/red) provides immediate visual feedback on compliance.
        - Conclusiones (Conclusions): Goal: Inform. Viz: Styled cards/blockquotes (HTML/CSS). Justification: Highlights the final takeaways, making them stand out and easy to remember.
        - All diagrams/icons use Unicode characters or are built with HTML/CSS. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #F8F9FA;
            color: #343A40;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 350px;
            margin-left: auto;
            margin-right: auto;
            height: auto;
            min-height: 300px;
        }
        @media (min-width: 640px) {
            .chart-container {
                min-height: 350px;
            }
        }
        .nav-link.active {
            color: #4F46E5; /* Indigo 600 */
            font-weight: 600;
        }
        .tab-btn.active {
            border-color: #4F46E5;
            color: #4F46E5;
            background-color: #EEF2FF;
        }
        .standard-item.active {
             background-color: #F9FAFB;
        }
        .standard-item .details {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-in-out, padding 0.5s ease-in-out;
            padding-top: 0;
            padding-bottom: 0;
        }
        .standard-item.active .details {
            max-height: 500px;
            padding-top: 1rem;
            padding-bottom: 1.25rem;
        }
    </style>
</head>
<body class="bg-[#FDFBF7] text-[#3D405B]">

    <header class="bg-[#FDFBF7]/80 backdrop-blur-lg sticky top-0 z-50 border-b border-gray-200">
        <nav class="container mx-auto px-4 lg:px-6 py-3">
            <div class="flex justify-between items-center">
                <a href="#inicio" class="text-xl font-bold text-indigo-600">SG-SST L&M</a>
                <div class="hidden md:flex items-center space-x-6">
                    <a href="#resumen" class="nav-link text-gray-600 hover:text-indigo-600 transition">Resumen</a>
                    <a href="#empresa" class="nav-link text-gray-600 hover:text-indigo-600 transition">La Empresa</a>
                    <a href="#evaluacion" class="nav-link text-gray-600 hover:text-indigo-600 transition">Evaluación</a>
                    <a href="#conclusiones" class="nav-link text-gray-600 hover:text-indigo-600 transition">Conclusiones</a>
                </div>
                <div class="md:hidden">
                    <select id="mobile-nav" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
                        <option value="#inicio">Inicio</option>
                        <option value="#resumen">Resumen</option>
                        <option value="#empresa">La Empresa</option>
                        <option value="#evaluacion">Evaluación</option>
                        <option value="#conclusiones">Conclusiones</option>
                    </select>
                </div>
            </div>
        </nav>
    </header>

    <main>
        <section id="inicio" class="py-20 md:py-28 bg-white">
            <div class="container mx-auto px-4 text-center">
                <h1 class="text-3xl md:text-5xl font-bold text-gray-800 leading-tight">Evaluación de Estándares Mínimos de Calidad del SG-SST</h1>
                <h2 class="text-xl md:text-2xl font-semibold text-indigo-600 mt-2">Consultorio Odontológico L&M</h2>
                <p class="mt-6 max-w-3xl mx-auto text-gray-600 text-lg">Un análisis interactivo sobre la implementación del Sistema de Gestión de Seguridad y Salud en el Trabajo, enfocado en proteger el bienestar del personal y cumplir con la normativa vigente.</p>
                <div class="mt-8 text-sm text-gray-500">
                    <p>Un reporte por: Noreza Abigail Gasca Bustamante & Laura Sofía Vargas Rojas</p>
                </div>
            </div>
        </section>

        <section id="resumen" class="py-16 lg:py-24">
            <div class="container mx-auto px-4">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-gray-800">Resumen Ejecutivo</h2>
                    <p class="mt-2 text-lg text-gray-600">Resultados clave de la evaluación del SG-SST.</p>
                </div>
                <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8 items-center">
                    <div class="lg:col-span-1 space-y-6">
                        <div class="bg-white p-6 rounded-xl shadow-md border border-gray-100">
                            <h3 class="font-semibold text-gray-700">Nivel de Riesgo</h3>
                            <p class="text-3xl font-bold text-indigo-600 mt-1">Riesgo I (1)</p>
                            <p class="text-sm text-gray-500 mt-1">Clasificación de bajo riesgo.</p>
                        </div>
                        <div class="bg-white p-6 rounded-xl shadow-md border border-gray-100">
                            <h3 class="font-semibold text-gray-700">Total de Trabajadores</h3>
                            <p class="text-3xl font-bold text-indigo-600 mt-1">6</p>
                            <p class="text-sm text-gray-500 mt-1">Incluyendo personal administrativo.</p>
                        </div>
                         <div class="bg-white p-6 rounded-xl shadow-md border border-red-200">
                            <h3 class="font-semibold text-red-800">Oportunidad de Mejora</h3>
                            <p class="text-lg font-bold text-red-600 mt-1">Plan Anual de Trabajo</p>
                            <p class="text-sm text-red-500 mt-1">El estándar clave que no se cumple actualmente.</p>
                        </div>
                    </div>
                    <div class="md:col-span-1 lg:col-span-2 bg-white p-6 rounded-xl shadow-lg border border-gray-100">
                        <h3 class="text-center text-xl font-semibold text-gray-700 mb-4">Cumplimiento de Estándares</h3>
                        <div class="chart-container">
                            <canvas id="complianceChart"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="empresa" class="py-16 lg:py-24 bg-gray-50">
            <div class="container mx-auto px-4">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-gray-800">Caracterización de la Empresa</h2>
                    <p class="mt-2 text-lg text-gray-600">Un vistazo a la estructura y funcionamiento del Consultorio Odontológico L&M.</p>
                </div>
                <div class="max-w-4xl mx-auto">
                    <div class="flex justify-center border-b border-gray-200 mb-8 space-x-2 sm:space-x-4">
                        <button class="tab-btn active py-3 px-4 sm:px-6 font-semibold text-gray-500 border-b-2 border-transparent transition" data-tab="estructura">Estructura</button>
                        <button class="tab-btn py-3 px-4 sm:px-6 font-semibold text-gray-500 border-b-2 border-transparent transition" data-tab="funcionamiento">Funcionamiento</button>
                    </div>
                    <div id="tab-content" class="bg-white p-6 sm:p-8 rounded-xl shadow-lg border border-gray-100">
                        <div id="estructura" class="tab-pane active">
                            <h3 class="text-xl font-bold mb-4 text-indigo-700">Estructura Física y de Seguridad</h3>
                            <div class="grid md:grid-cols-2 gap-8">
                                <div>
                                    <h4 class="font-semibold mb-2 text-gray-700">Ubicación</h4>
                                    <p class="text-gray-600">Carrera 5 #12-09, Oficina 501, Edificio Calle Real, Neiva-Huila.</p>
                                    <h4 class="font-semibold mt-6 mb-2 text-gray-700">Espacios</h4>
                                    <ul class="space-y-1 text-gray-600 list-disc list-inside">
                                        <li>Oficinas: 1, Cubículos: 4, Baños: 1, Cocina: 1, Almacenamiento: 1, Espera: 1</li>
                                    </ul>
                                </div>
                                <div>
                                    <h4 class="font-semibold mb-2 text-gray-700">Equipamiento de Seguridad</h4>
                                    <ul class="space-y-1 text-gray-600 list-disc list-inside">
                                        <li>Señalización de ruta de evacuación</li>
                                        <li>Extintores: 2 multipropósito, 1 solkaflam 123</li>
                                        <li>Kit de primeros auxilios y Gabinete de incendios</li>
                                        <li>Luces y Sistemas de emergencia</li>
                                        <li>Cámaras de seguridad</li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                        <div id="funcionamiento" class="tab-pane hidden">
                            <h3 class="text-xl font-bold mb-4 text-indigo-700">Operación y Personal</h3>
                            <div class="grid md:grid-cols-2 gap-8">
                                <div>
                                    <h4 class="font-semibold mb-2 text-gray-700">Personal (6 en total)</h4>
                                    <ul class="space-y-1 text-gray-600 list-disc list-inside">
                                        <li>Gerente, Contador público, Aux. cartera, Aux. administrativo, Aux. tesorería, Servicios generales</li>
                                    </ul>
                                </div>
                                <div>
                                    <h4 class="font-semibold mb-2 text-gray-700">Detalles Operativos</h4>
                                    <ul class="space-y-2 text-gray-600">
                                        <li><span class="font-medium">Actividad:</span> Fondo de empleados (aporte, ahorro, créditos).</li>
                                        <li><span class="font-medium">ARL Asociada:</span> Equidad.</li>
                                        <li><span class="font-medium">Vigilancia:</span> 24h, provista por el edificio.</li>
                                        <li><span class="font-medium">Horario:</span> L-V, 7am-12pm y 2pm-6pm.</li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        
        <section id="evaluacion" class="py-16 lg:py-24">
            <div class="container mx-auto px-4">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-gray-800">Evaluación de Estándares Mínimos</h2>
                    <p class="mt-2 text-lg text-gray-600">Análisis detallado de cada estándar. Haz clic en cada uno para ver los detalles.</p>
                </div>
                <div class="max-w-4xl mx-auto bg-white rounded-xl shadow-lg border border-gray-100 divide-y divide-gray-200">
                    
                    <div class="standard-item cursor-pointer p-5" data-standard="1">
                        <div class="flex justify-between items-center">
                            <h3 class="font-semibold text-lg text-gray-800">1. Asignación de persona que diseña el SG-SST</h3>
                            <div class="flex items-center space-x-4">
                               <span class="text-sm font-bold text-green-600 bg-green-100 px-3 py-1 rounded-full">CUMPLE</span>
                                <span class="text-gray-400 transform transition-transform duration-300 chevron">▼</span>
                            </div>
                        </div>
                        <div class="details text-gray-600 border-l-4 border-green-500 pl-4 mt-2">La empresa cuenta con un auxiliar administrativo con más de un año de experiencia para esta función, garantizando un ambiente laboral seguro y el cumplimiento normativo.</div>
                    </div>

                    <div class="standard-item cursor-pointer p-5" data-standard="2">
                        <div class="flex justify-between items-center">
                            <h3 class="font-semibold text-lg text-gray-800">2. Afiliación al Sistema de Seguridad Social Integral</h3>
                             <div class="flex items-center space-x-4">
                                <span class="text-sm font-bold text-green-600 bg-green-100 px-3 py-1 rounded-full">CUMPLE</span>
                                <span class="text-gray-400 transform transition-transform duration-300 chevron">▼</span>
                            </div>
                        </div>
                        <div class="details text-gray-600 border-l-4 border-green-500 pl-4 mt-2">Se verificaron los registros que confirman la adhesión de todos los trabajadores, asegurando su acceso a servicios médicos y otras prestaciones de ley.</div>
                    </div>
                    
                    <div class="standard-item cursor-pointer p-5" data-standard="3">
                        <div class="flex justify-between items-center">
                            <h3 class="font-semibold text-lg text-gray-800">3. Capacitación en SST</h3>
                             <div class="flex items-center space-x-4">
                                <span class="text-sm font-bold text-green-600 bg-green-100 px-3 py-1 rounded-full">CUMPLE</span>
                                <span class="text-gray-400 transform transition-transform duration-300 chevron">▼</span>
                            </div>
                        </div>
                        <div class="details text-gray-600 border-l-4 border-green-500 pl-4 mt-2">Se ha realizado y documentado la formación adecuada al personal sobre los peligros y riesgos asociados a su trabajo, mediante documentos y presentaciones.</div>
                    </div>
                    
                    <div class="standard-item cursor-pointer p-5" data-standard="4">
                        <div class="flex justify-between items-center">
                            <h3 class="font-semibold text-lg text-gray-800">4. Plan anual de trabajo</h3>
                             <div class="flex items-center space-x-4">
                                <span class="text-sm font-bold text-red-600 bg-red-100 px-3 py-1 rounded-full">NO CUMPLE</span>
                                <span class="text-gray-400 transform transition-transform duration-300 chevron">▼</span>
                            </div>
                        </div>
                        <div class="details text-gray-600 border-l-4 border-red-500 pl-4 mt-2">Actualmente la empresa no cuenta con un plan de trabajo anual. Esta es la principal falencia, pues dificulta la guía estratégica, la asignación de recursos y la medición del desempeño del sistema.</div>
                    </div>
                    
                    <div class="standard-item cursor-pointer p-5" data-standard="5">
                        <div class="flex justify-between items-center">
                            <h3 class="font-semibold text-lg text-gray-800">5. Evaluaciones médicas ocupacionales</h3>
                            <div class="flex items-center space-x-4">
                                <span class="text-sm font-bold text-green-600 bg-green-100 px-3 py-1 rounded-full">CUMPLE</span>
                                <span class="text-gray-400 transform transition-transform duration-300 chevron">▼</span>
                            </div>
                        </div>
                        <div class="details text-gray-600 border-l-4 border-green-500 pl-4 mt-2">La empresa realiza y documenta los exámenes médicos de preingreso, periódicos y de retiro, así como en situaciones de incapacidad, para prevenir enfermedades laborales.</div>
                    </div>
                    
                    <div class="standard-item cursor-pointer p-5" data-standard="6">
                        <div class="flex justify-between items-center">
                            <h3 class="font-semibold text-lg text-gray-800">6. Identificación y valoración de riesgos</h3>
                             <div class="flex items-center space-x-4">
                                <span class="text-sm font-bold text-green-600 bg-green-100 px-3 py-1 rounded-full">CUMPLE</span>
                                <span class="text-gray-400 transform transition-transform duration-300 chevron">▼</span>
                            </div>
                        </div>
                        <div class="details text-gray-600 border-l-4 border-green-500 pl-4 mt-2">Junto a la ARL Equidad Seguros, se han identificado y valorado los peligros (ergonomía, iluminación, etc.), y la información está disponible para todo el personal.</div>
                    </div>
                    
                    <div class="standard-item cursor-pointer p-5" data-standard="7">
                        <div class="flex justify-between items-center">
                            <h3 class="font-semibold text-lg text-gray-800">7. Medidas de prevención y control</h3>
                             <div class="flex items-center space-x-4">
                                <span class="text-sm font-bold text-green-600 bg-green-100 px-3 py-1 rounded-full">CUMPLE</span>
                                <span class="text-gray-400 transform transition-transform duration-300 chevron">▼</span>
                            </div>
                        </div>
                        <div class="details text-gray-600 border-l-4 border-green-500 pl-4 mt-2">Se realiza capacitación integral para que los empleados reconozcan y gestionen riesgos, incluyendo estrés laboral, riesgos psicosociales y uso de equipos de emergencia.</div>
                    </div>

                </div>
            </div>
        </section>

        <section id="conclusiones" class="py-16 lg:py-24 bg-gray-50">
            <div class="container mx-auto px-4">
                <div class="text-center mb-12">
                    <h2 class="text-3xl font-bold text-gray-800">Conclusiones Clave</h2>
                    <p class="mt-2 text-lg text-gray-600">Principales hallazgos y perspectivas de la evaluación.</p>
                </div>
                <div class="grid md:grid-cols-2 gap-8 max-w-5xl mx-auto">
                    <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-indigo-500">
                        <p class="text-gray-700">La asignación de una persona encargada del SG-SST demuestra un <span class="font-semibold">compromiso claro con la implementación</span> y mejora continua de prácticas seguras.</p>
                    </div>
                     <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-red-500">
                        <p class="text-gray-700">A pesar de los logros, la <span class="font-semibold">ausencia de un Plan Anual de Trabajo</span> resalta como la oportunidad de mejora más importante para estructurar la planificación y ejecución.</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-green-500">
                        <p class="text-gray-700">La empresa evidencia un <span class="font-semibold">cumplimiento satisfactorio</span> en afiliación al SSSI y capacitaciones, subrayando la importancia que se le da al bienestar de los trabajadores.</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-blue-500">
                        <p class="text-gray-700">Las evaluaciones médicas y medidas preventivas reflejan un <span class="font-semibold">enfoque proactivo</span> hacia la identificación y mitigación de riesgos, consolidando la protección del personal.</p>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <footer class="bg-white border-t border-gray-200 mt-16">
        <div class="container mx-auto py-6 px-4 text-center text-gray-500">
            <p>&copy; 2024 Informe Interactivo SG-SST L&M. Todos los derechos reservados.</p>
        </div>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            
            const complianceData = {
                labels: ['Cumplidos', 'No Cumplidos'],
                datasets: [{
                    label: 'Cumplimiento de Estándares',
                    data: [6, 1],
                    backgroundColor: [
                        '#10B981', // green-500
                        '#EF4444'  // red-500
                    ],
                    borderColor: '#FFFFFF',
                    borderWidth: 4,
                    hoverOffset: 8
                }]
            };
            const complianceConfig = {
                type: 'doughnut',
                data: complianceData,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    cutout: '70%',
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                font: {
                                    size: 14,
                                    family: 'Inter, sans-serif'
                                }
                            }
                        },
                        tooltip: {
                            bodyFont: {
                                size: 14,
                                family: 'Inter, sans-serif'
                            },
                            titleFont: {
                                size: 16,
                                family: 'Inter, sans-serif'
                            }
                        }
                    }
                }
            };
            const complianceChart = new Chart(
                document.getElementById('complianceChart'),
                complianceConfig
            );

            const tabBtns = document.querySelectorAll('.tab-btn');
            const tabPanes = document.querySelectorAll('.tab-pane');
            tabBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    const tabId = btn.getAttribute('data-tab');
                    tabBtns.forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    tabPanes.forEach(pane => {
                        if (pane.id === tabId) {
                            pane.classList.remove('hidden');
                            pane.classList.add('active');
                        } else {
                            pane.classList.add('hidden');
                            pane.classList.remove('active');
                        }
                    });
                });
            });

            const standardItems = document.querySelectorAll('.standard-item');
            standardItems.forEach(item => {
                item.addEventListener('click', () => {
                    const chevron = item.querySelector('.chevron');
                    if (item.classList.contains('active')) {
                        item.classList.remove('active');
                        chevron.style.transform = 'rotate(0deg)';
                    } else {
                        item.classList.add('active');
                        chevron.style.transform = 'rotate(180deg)';
                    }
                });
            });

            const mobileNav = document.getElementById('mobile-nav');
            mobileNav.addEventListener('change', (e) => {
                window.location.href = e.target.value;
            });
            
            const sections = document.querySelectorAll('section');
            const navLinks = document.querySelectorAll('header .nav-link');
            const onScroll = () => {
                let current = '';
                sections.forEach(section => {
                    const sectionTop = section.offsetTop;
                    if (pageYOffset >= sectionTop - 100) {
                        current = section.getAttribute('id');
                    }
                });
                
                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href').includes(current)) {
                        link.classList.add('active');
                    }
                });
            };
            window.addEventListener('scroll', onScroll);
        });
    </script>
</body>
</html>
