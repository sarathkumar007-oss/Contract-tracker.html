    body {
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Arial, sans-serif;
        background: #f5f5f5;
        padding: 10px;
    }
    
    .header {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
        padding: 20px;
        border-radius: 12px;
        margin-bottom: 20px;
        box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    
    .header h1 {
        font-size: 24px;
        margin-bottom: 5px;
    }
    
    .header .subtitle {
        font-size: 14px;
        opacity: 0.9;
    }
    
    .stats {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 10px;
        margin-bottom: 20px;
    }
    
    .stat-card {
        background: white;
        padding: 15px;
        border-radius: 8px;
        box-shadow: 0 2px 4px rgba(0,0,0,0.08);
    }
    
    .stat-card .number {
        font-size: 32px;
        font-weight: bold;
        color: #667eea;
    }
    
    .stat-card .label {
        font-size: 12px;
        color: #666;
        margin-top: 5px;
    }
    
    .contract-card {
        background: white;
        padding: 15px;
        margin-bottom: 12px;
        border-radius: 8px;
        border-left: 4px solid;
        box-shadow: 0 2px 4px rgba(0,0,0,0.08);
    }
    
    .contract-card.urgent {
        border-left-color: #ff4444;
    }
    
    .contract-card.warning {
        border-left-color: #ffaa00;
    }
    
    .contract-card.active {
        border-left-color: #44ff44;
    }
    
    .contract-card h3 {
        font-size: 16px;
        margin-bottom: 8px;
        color: #333;
    }
    
    .contract-meta {
        font-size: 13px;
        color: #666;
        margin-bottom: 8px;
    }
    
    .contract-meta span {
        margin-right: 12px;
    }
    
    .progress-input {
        width: 100%;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 6px;
        font-size: 14px;
        margin-top: 8px;
        font-family: inherit;
    }
    
    .btn {
        background: #667eea;
        color: white;
        border: none;
        padding: 10px 20px;
        border-radius: 6px;
        font-size: 14px;
        font-weight: 600;
        cursor: pointer;
        width: 100%;
        margin-top: 8px;
    }
    
    .btn:active {
        background: #5568d3;
    }
    
    .btn-complete {
        background: #44ff44;
        color: #333;
    }
    
    .section-title {
        font-size: 18px;
        font-weight: bold;
        margin: 20px 0 10px 0;
        color: #333;
    }
    
    .empty-state {
        text-align: center;
        padding: 40px 20px;
        color: #999;
    }
    
    .quick-add {
        position: fixed;
        bottom: 20px;
        right: 20px;
        width: 60px;
        height: 60px;
        background: #667eea;
        color: white;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 32px;
        box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
        cursor: pointer;
    }
    
    .modal {
        display: none;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0,0,0,0.5);
        align-items: center;
        justify-content: center;
        padding: 20px;
    }
    
    .modal.active {
        display: flex;
    }
    
    .modal-content {
        background: white;
        padding: 20px;
        border-radius: 12px;
        width: 100%;
        max-width: 500px;
        max-height: 90vh;
        overflow-y: auto;
    }
    
    .form-group {
        margin-bottom: 15px;
    }
    
    .form-group label {
        display: block;
        font-size: 14px;
        font-weight: 600;
        margin-bottom: 5px;
        color: #333;
    }
    
    .form-group input,
    .form-group select,
    .form-group textarea {
        width: 100%;
        padding: 10px;
        border: 1px solid #ddd;
        border-radius: 6px;
        font-size: 14px;
        font-family: inherit;
    }
</style>
