import React from 'react';
import axios from 'axios';

export default function UploadImage() {
  async function handleUpload(e) {
    const file = e.target.files?.[0];
    if (!file) return;
    const fd = new FormData();
    fd.append('image', file);
    try {
      const resp = await axios.post('/api/vision/upload', fd, { headers: { 'Content-Type': 'multipart/form-data' } });
      alert('Image processed: ' + JSON.stringify(resp.data));
    } catch (err) {
      alert('Image processing failed: ' + (err.response?.data?.error || err.message));
    }
  }
  return (
    <div>
      <h3>Upload Image</h3>
      <input type="file" accept="image/*" onChange={handleUpload} />
    </div>
  );
}
